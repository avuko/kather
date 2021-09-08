FROM ubuntu:latest

# Env & Arg variables
USER root
ARG USERNAME=kather
EXPOSE 22
# Apt update & apt install required packages
RUN apt update && apt -y install openssh-server whois sudo

# Add a non-root user & set password
RUN useradd -ms /bin/bash $USERNAME

# Remove no-needed packages
RUN apt purge -y whois && apt -y autoremove && apt -y autoclean && apt -y clean

# Copy the entrypoint
COPY entrypoint.sh entrypoint.sh
RUN chmod +x /entrypoint.sh

# Create the ssh directory and authorized_keys file
USER $USERNAME
RUN mkdir /home/$USERNAME/.ssh
COPY ./katherkey.pub /home/$USERNAME/.ssh/authorized_keys

USER root
RUN chown $USERNAME /home/$USERNAME/.ssh/authorized_keys && \
    chmod 600 /home/$USERNAME/.ssh/authorized_keys
RUN echo "${USERNAME} ALL=(ALL) NOPASSWD: ALL " >> /etc/sudoers

# Run entrypoint
# ENTRYPOINT  "/usr/sbin/sshd -D -o 'ListenAddress=0.0.0.0'"
# CMD ["/usr/sbin/sshd", "-D", "-o", "ListenAddress=0.0.0.0"]
CMD ["./entrypoint.sh"]
