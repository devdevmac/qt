FROM ubuntu:16.04
LABEL maintainer therecipe

ENV USER user
ENV HOME /home/$USER
ENV GOPATH $HOME/work
ENV PATH /usr/lib/mxe/usr/bin:/usr/local/go/bin:$PATH
ENV QT_DIR /opt/Qt
ENV QT_DOCKER true
ENV QT_MXE true
ENV QT_MXE_ARCH 386
ENV QT_MXE_STATIC false

COPY --from=therecipe/qt:linux /usr/local/go /usr/local/go
COPY --from=therecipe/qt:linux $GOPATH/bin $GOPATH/bin
COPY --from=therecipe/qt:linux $GOPATH/src/github.com/therecipe/qt $GOPATH/src/github.com/therecipe/qt
COPY --from=therecipe/qt:linux /opt/Qt/5.11.1/gcc_64/include /opt/Qt/5.11.1/gcc_64/include
COPY --from=therecipe/qt:windows_32_shared_base_7 /usr/lib/mxe /usr/lib/mxe

RUN $GOPATH/bin/qtsetup prep
RUN $GOPATH/bin/qtsetup check windows
RUN $GOPATH/bin/qtsetup generate windows
RUN $GOPATH/bin/qtsetup install windows
RUN cd $GOPATH/src/github.com/therecipe/qt/internal/examples/widgets/line_edits && $GOPATH/bin/qtdeploy build windows && rm -rf ./deploy
