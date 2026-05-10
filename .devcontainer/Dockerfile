FROM debian:bookworm-slim
COPY setup.sh /tmp/setup.sh
COPY config.json /etc/xray/g2ray.json
COPY show-link.sh /usr/local/bin/show-link.sh
COPY start.sh /usr/local/bin/start.sh
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
       bash curl wget unzip ca-certificates openssl uuid-runtime tmux \
    && rm -rf /var/lib/apt/lists/* \
    && mkdir -p /etc/xray \
    && chmod +x /tmp/setup.sh \
    && /tmp/setup.sh \
    && rm /tmp/setup.sh \
    && chmod +x /usr/local/bin/show-link.sh \
    && chmod +x /usr/local/bin/start.sh
EXPOSE 443
CMD ["/usr/local/bin/xray","run","-c","/etc/xray/g2ray.json"]
#!/bin/bash
tmux kill-session -t g2ray 2>/dev/null || true
tmux new-session -d -s g2ray
tmux send-keys -t g2ray "sudo /usr/local/bin/xray run -c /etc/xray/g2ray.json >/tmp/xray.log" Enter
sleep 2 && show-link.sh
EOF
sudo chmod +x /usr/local/bin/start.sh 
