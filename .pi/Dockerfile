FROM faddat/sos-lite

COPY motd /etc/motd

COPY seahorse.service /etc/systemd/system/seahorse.service


# due to a high death rate among fry, enterprising fry should make their own zt networks, and consider adding i2p, tinc and others.
# The original meshbird may have been more compelling, as it allowed to join a network with out a coordinator.  Fry should explore before being eaten by sharks. 




RUN sed -i -e "s/^CheckSpace/#!!!CheckSpace/g" /etc/pacman.conf && \
        # Dependencies & monitoring tools
        pacman -Syyu --noconfirm wget sudo base-devel go git yarn npm zerotier-one && \
        # Install Seahorse
        wget https://github.com/seatoshi/seahorse/releases/download/latest/seahorse_latest_linux_arm64.tar.gz && \
        tar xvf seahorse_latest_linux_arm64.tar.gz && \
        mv seahorsed /usr/bin/seahorsed && \
        chmod +x /usr/bin/seahorsed && \
        systemctl enable seahorse.service && \
	systemctl enable zerotier-one && \
	echo 'seahorsed init fry$RANDOM' >> /usr/local/bin/firstboot.sh && \
  	echo "wget https://github.com/seatoshi/seahorse/raw/master/genesis.json" >> /usr/local/bin/firstboot.sh && \
  	echo "cp genesis.json /root/.seahorse/config" && \
	echo "zerotier-cli join 1d71939404e366e8" >> /usr/local/bin/firstboot.sh
	
	
RUN sed -i -e "s/^#!!!CheckSpace/CheckSpace/g" /etc/pacman.conf

