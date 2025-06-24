# ===============================================================================================================
# Docker file for indyscan-daemon-ocp
#
# Configures the environment and permissions necessary for indyscan-daemon to run on OpenShift.
#
# To Build:
#  docker build --no-cache -f ./Dockerfile -t indyscan-daemon-ocp:4.6.1 .
#
# Push to OpenShift using https://github.com/bcgov/openshift-developer-tools:
#  oc-push-image.sh -i indyscan-daemon-ocp:4.6.1 -n ca7f8f-tools -r image-registry.apps.silver.devops.gov.bc.ca
# ---------------------------------------------------------------------------------------------------------------
FROM ghcr.io/patrik-stas/indyscan/indyscan-daemon:4.6.1

# Required for OpenShift environments due to how npm and the modules have been installed.
ENV HOME=/home/indyscan

USER root

# - In order to drop the root user, we have to make some directories writable
#   to the root group as OpenShift default security model is to run the container
#   under random UID.
RUN addgroup indyscan root

# The root group needs access the directories under /home/indyscan for the container to function in OpenShift.
RUN chown -R indyscan:root /home/indyscan && \
    chmod -R ug+rw /home/indyscan

USER indyscan
