FROM buildpack-deps:buster

ENV DEBIAN_FRONTEND noninteractive

# we need wine for this all to work, Use APT repo
RUN set -x \
    && dpkg --add-architecture i386 \
    && apt update \
    && apt -y install --install-recommends wine-development xvfb xauth cabextract winbind rename \
    && apt-get clean \
    && wget -nv -O /usr/local/bin/winetricks 'https://raw.githubusercontent.com/Winetricks/winetricks/master/src/winetricks' \
    && chmod +x /usr/local/bin/winetricks

ARG PYTHON_VERSION=3.7.5
ARG PYINSTALLER_VERSION=3.6

# wine settings
ENV WINEARCH win32
ENV WINEDEBUG fixme-all
ENV WINEPREFIX /wine

# PYPI repository location
ENV PYPI_URL=https://pypi.python.org/
# PYPI index location
ENV PYPI_INDEX_URL=https://pypi.python.org/simple

# install python in wine, using the msi packages to install, extracting
# the files directly, since installing isn't running correctly.
RUN set -x \
    && winetricks win7 \
    && for msifile in `echo core dev exe lib path pip tcltk tools`; do \
        wget -nv "https://www.python.org/ftp/python/$PYTHON_VERSION/win32/${msifile}.msi"; \
        wine msiexec /i "${msifile}.msi" /qb TARGETDIR=C:/Python37; \
        rm ${msifile}.msi; \
    done \
    && cd /wine/drive_c/Python37 \
    && echo 'wine '\''C:\Python37\python.exe'\'' "$@"' > /usr/bin/python \
    && echo 'wine '\''C:\Python37\Scripts\easy_install.exe'\'' "$@"' > /usr/bin/easy_install \
    && echo 'wine '\''C:\Python37\Scripts\pip.exe'\'' "$@"' > /usr/bin/pip \
    && echo 'wine '\''C:\Python37\Scripts\pyinstaller.exe'\'' "$@"' > /usr/bin/pyinstaller \
    && echo 'wine '\''C:\Python37\Scripts\pyupdater.exe'\'' "$@"' > /usr/bin/pyupdater \
    && echo 'wine '\''C:\Python37\Scripts\\tox.exe'\'' "$@"' > /usr/bin/tox \
    && echo 'assoc .py=PythonScript' | wine cmd \
    && echo 'ftype PythonScript=c:\Python37\python.exe "%1" %*' | wine cmd \
    && while pgrep wineserver >/dev/null; do echo "Waiting for wineserver"; sleep 1; done \
    && chmod +x /usr/bin/python /usr/bin/easy_install /usr/bin/pip /usr/bin/pyinstaller /usr/bin/pyupdater /usr/bin/tox \
    && (pip install -U pip || true) \
    && pip install tox nose coverage \
    && rm -rf /tmp/.wine-*

ENV W_DRIVE_C=/wine/drive_c
ENV W_WINDIR_UNIX="$W_DRIVE_C/windows"
ENV W_SYSTEM_DLLS="$W_WINDIR_UNIX/system32"
ENV W_TMP="$W_DRIVE_C/windows/temp/_$0"

# install Microsoft Visual C++ Redistributable for Visual Studio 2017 dll files
RUN set -x \
    && rm -f "$W_TMP"/* \
    && wget -P "$W_TMP" https://download.visualstudio.microsoft.com/download/pr/11687613/88b50ce70017bf10f2d56d60fcba6ab1/VC_redist.x86.exe \
    && cabextract -q --directory="$W_TMP" "$W_TMP"/VC_redist.x86.exe \
    && cabextract -q --directory="$W_TMP" "$W_TMP/a10" \
    && cabextract -q --directory="$W_TMP" "$W_TMP/a11" \
    && cd "$W_TMP" \
    && rename 's/_/\-/g' *.dll \
    && cp "$W_TMP"/*.dll "$W_SYSTEM_DLLS"/

# install pyinstaller
RUN /usr/bin/pip install pyinstaller==$PYINSTALLER_VERSION
