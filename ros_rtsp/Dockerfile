ARG ROS_DISTRO

# ---

FROM ros:${ROS_DISTRO}-ros-base

RUN apt-get update && apt-get install locales
RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8

ENV PYTHONUNBUFFERED=1

RUN apt-get update && apt-get install -y \
    && rm -rf /var/likb/apt/lists/*

COPY . /hr_ws/src/rtsp/
WORKDIR /hr_ws

RUN /bin/bash -c 'apt-get install -y libgstreamer1.0-0 gstreamer1.0-plugins-base gstreamer1.0-plugins-good gstreamer1.0-plugins-bad gstreamer1.0-plugins-ugly gstreamer1.0-libav gstreamer1.0-doc gstreamer1.0-tools gstreamer1.0-x gstreamer1.0-alsa gstreamer1.0-gl gstreamer1.0-gtk3 gstreamer1.0-qt5 gstreamer1.0-pulseaudio'
RUN /bin/bash -c 'apt-get install -y libgstreamer-plugins-base1.0-dev libgstreamer-plugins-good1.0-dev libgstreamer-plugins-bad1.0-dev libgstrtspserver-1.0-dev'

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
    roslaunch ros_rtsp rtsp_streams.launch'

