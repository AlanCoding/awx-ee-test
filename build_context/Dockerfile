ARG TAG=devel

FROM quay.io/alancoding/ansible-runner:${TAG}

RUN pip3 install --no-cache-dir --upgrade pip setuptools
ADD requirements.yml /build/

RUN ansible-galaxy role install -r /build/requirements.yml --roles-path /usr/share/ansible/roles
RUN ansible-galaxy collection install -r /build/requirements.yml --collections-path /usr/share/ansible/collections
ADD bindep_output.txt /build/
RUN dnf -y install $(cat /build/bindep_output.txt) && dnf clean all && rm -rf /var/cache/dnf
ADD requirements_combined.txt /build/
RUN pip3 install --no-cache-dir --upgrade -r /build/requirements_combined.txt
