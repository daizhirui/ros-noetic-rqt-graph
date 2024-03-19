pkgdesc="ROS - rqt_graph provides a GUI plugin for visualizing the ROS computation graph."
url='https://wiki.ros.org/rqt_graph'

pkgname='ros-noetic-rqt-graph'
pkgver='0.4.14'
arch=('any')
pkgrel=2
license=('BSD')

ros_makedepends=(
    ros-noetic-catkin
)

makedepends=(
    cmake
    ros-build-tools
    ${ros_makedepends[@]}
)

ros_depends=(
    ros-noetic-rqt-gui-py
    ros-noetic-rosservice
    ros-noetic-rqt-gui
    ros-noetic-rosnode
    ros-noetic-rosgraph-msgs
    ros-noetic-rostopic
    ros-noetic-rosgraph
    ros-noetic-python-qt-binding
    ros-noetic-qt-dotgraph
    ros-noetic-rospy
    ros-noetic-roslib
)

depends=(
    ${ros_depends[@]}
    python-rospkg
)

_commit="759e210ac03a9c19e3ed4040361f97499203191f"
_dir="rqt_graph-${_commit}"
source=("${pkgname}-${pkgver}.tar.gz"::"https://github.com/ros-visualization/rqt_graph/archive/${_commit}.tar.gz")
sha256sums=('57d37b075d32522d8efc71285e314900c76e3bd0ee58c49aeed0833b5c7a9131')

build() {
    # Use ROS environment variables.
    source /usr/share/ros-build-tools/clear-ros-env.sh
    [ -f /opt/ros/noetic/setup.bash ] && source /opt/ros/noetic/setup.bash

    # Create the build directory.
    [ -d ${srcdir}/build ] || mkdir ${srcdir}/build
    cd ${srcdir}/build

    # Build the project.
    cmake ${srcdir}/${_dir} \
        -DCATKIN_BUILD_BINARY_PACKAGE=ON \
        -DCMAKE_INSTALL_PREFIX=/opt/ros/noetic \
        -DPYTHON_EXECUTABLE=/usr/bin/python \
        -DSETUPTOOLS_DEB_LAYOUT=OFF
    make
}

package() {
    cd "${srcdir}/build"
    make DESTDIR="${pkgdir}/" install
}
