# Publish ROS image topic to RTSP

This example demonstrates how to publish a ROS image topic using an RTSP server. The example spawns two nodes: The first one uses the usb_cam package to acquire an image from /dev/video0 and publish as a ROS image topic. The second one listens to the image topic and makes it available as a RTSP stream.


You'll need to have docker and docker-compose installed.

    git clone git@github.com:CERTH-ITI/ros_rtsp_publisher_example.git
    cd ros_rtsp_publisher_example
    sudo docker-compose up

Your stream is available at rtsp://0.0.0.0:8554/back

