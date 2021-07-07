FROM faddat/sos-lite

COPY motd /etc/motd

COPY seahorse.service /etc/systemd/system/seahorse.service

RUN sed -i -e "s/^CheckSpace/#!!!CheckSpace/g" /etc/pacman.conf && \
        # Dependencies & monitoring tools
        pacman -Syyu --noconfirm wget sudo base-devel go git yarn npm && \
        # Install Seahorse
        wget https://github.com/seatoshi/seahorse/releases/download/latest/seahorse_latest_linux_arm64.tar.gz && \
        tar xvf seahorse_latest_linux_arm64.tar.gz && \
        mv seahorsed /usr/bin/seahorsed && \
        chmod +x /usr/bin/seahorsed && \
        systemctl enable seahorse.service && \
	echo 'seahorsed init fry$RANDOM' >> /usr/local/bin/firstboot.sh && \
  ehco 'wget https://github.com/seatoshi/seahorse/raw/master/genesis.json' >> /usr/local/bin/firstboot/sh && \
  echo 'cp genesis.json /root/.seahorse/config'
        sed -i -e "s/^#!!!CheckSpace/CheckSpace/g" /etc/pacman.conf

