ARG ROS_DISTRO

# ---

FROM ros:${ROS_DISTRO}-ros-base

RUN apt-get update && apt-get install locales
RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8

ENV PYTHONUNBUFFERED=1

RUN apt-get update && apt-get install -y \
    && rm -rf /var/likb/apt/lists/*

COPY . /hr_ws/src/usb_cam/
WORKDIR /hr_ws

RUN /bin/bash -c '. /opt/ros/$ROS_DISTRO/setup.bash; \
    catkin_make; \
    source devel/setup.bash; \
    rosdep init; \
    rosdep update; \
    rosdep install --from-paths src --ignore-src -r -y'

# RUN /bin/bash -c '. /opt/ros/$ROS_DISTRO/setup.bash; catkin_make'
# RUN /bin/bash -c '. /opt/ros/$ROS_DISTRO/setup.bash; source devel/setup.bash'

# Do a catkin_make everytime we run to catch changes in src
CMD /bin/bash -c '. /opt/ros/$ROS_DISTRO/setup.bash; \
    catkin_make; \
    source devel/setup.bash; \
    roslaunch usb_cam usb_cam-test.launch'

