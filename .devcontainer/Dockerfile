# Week 5 P4 lab environment: the official P4 compiler and BMv2 software switch, plus Mininet.
# x86 only, like the upstream image — GitHub Codespaces runs on x86.
#
# Build and publish (course staff):
#   docker build --platform linux/amd64 -t firdaussahran/netlab-p4:1.0 .devcontainer
FROM p4lang/p4c:latest

RUN apt-get update \
 && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
      mininet iputils-ping iproute2 tcpdump git less nano \
 && rm -rf /var/lib/apt/lists/*

# The image's Python (a virtualenv, first on PATH) has Scapy and the BMv2 CLI's libraries;
# Mininet installed into the system Python. Let the virtualenv see it too.
RUN SITE=$(/root/p4-python-venv/bin/python3 -c 'import site; print(site.getsitepackages()[0])') \
 && echo /usr/lib/python3/dist-packages > "$SITE/system-dist-packages.pth" \
 && /root/p4-python-venv/bin/python3 -c 'import mininet.net, scapy.all'

WORKDIR /workspaces
CMD ["bash"]
