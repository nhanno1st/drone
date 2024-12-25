1. Cài đặt ROS
Đảm bảo bạn đã cài đặt ROS trên máy tính của mình. Dưới đây là hướng dẫn nhanh cho các phiên bản phổ biến:

ROS Noetic (Ubuntu 20.04):
bash
Copy code
sudo apt update
sudo apt install ros-noetic-desktop-full
ROS Melodic (Ubuntu 18.04):
bash
Copy code
sudo apt update
sudo apt install ros-melodic-desktop-full
2. Tạo một ROS Workspace
Nếu bạn chưa có workspace, hãy tạo một workspace mới:

bash
Copy code
mkdir -p ~/catkin_ws/src
cd ~/catkin_ws
catkin_make
source devel/setup.bash
Thêm lệnh source vào file .bashrc để tự động tải ROS khi mở terminal:

bash
Copy code
echo "source ~/catkin_ws/devel/setup.bash" >> ~/.bashrc
source ~/.bashrc
3. Clone Repository
Tải về mã nguồn của hector_quadrotor từ GitHub vào thư mục src trong workspace:

bash
Copy code
cd ~/catkin_ws/src
git clone https://github.com/tu-darmstadt-ros-pkg/hector_quadrotor.git
4. Cài đặt các Dependencies
Dùng rosdep để tự động cài đặt các gói phụ thuộc:

bash
Copy code
cd ~/catkin_ws
rosdep install --from-paths src --ignore-src -r -y
Nếu gặp lỗi, hãy chắc chắn rằng rosdep đã được cài đặt và cấu hình:

bash
Copy code
sudo apt install python3-rosdep
sudo rosdep init
rosdep update
5. Build Workspace
Sau khi cài đặt dependencies, build workspace:

bash
Copy code
cd ~/catkin_ws
catkin_make
6. Kiểm tra Tệp Launch
Kiểm tra các tệp launch có sẵn trong gói:

bash
Copy code
roscd hector_quadrotor_gazebo/launch
ls
Bạn sẽ thấy các tệp như:

quadrotor_empty_world.launch
spawn_quadrotor.launch
7. Chạy Project
Dưới đây là các lệnh cơ bản để chạy project:

Chạy mô phỏng Gazebo với quadrotor:
bash
Copy code
roslaunch hector_quadrotor_gazebo quadrotor_empty_world.launch
Spawn quadrotor vào thế giới Gazebo:
bash
Copy code
roslaunch hector_quadrotor_gazebo spawn_quadrotor.launch
8. Điều khiển Quadrotor
Bạn có thể điều khiển quadrotor bằng cách sử dụng các lệnh ROS:

Điều khiển thủ công với keyboard teleop:
Chạy teleop node:
bash
Copy code
rosrun teleop_twist_keyboard teleop_twist_keyboard.py
Đảm bảo rằng bạn đã kết nối node điều khiển tới quadrotor:
bash
Copy code
rostopic pub /cmd_vel geometry_msgs/Twist '[linear]' '[angular]'
9. Xử lý Lỗi Thường Gặp
Tệp launch không tồn tại:

Đảm bảo bạn đã clone đúng repository và build workspace thành công.
Kiểm tra trong ~/catkin_ws/src/hector_quadrotor/hector_quadrotor_gazebo/launch.
Gazebo không chạy:

Cài đặt plugin Gazebo:
bash
Copy code
sudo apt install ros-$ROS_DISTRO-gazebo-ros
Lỗi rosdep không cài được dependencies:

Cài đặt dependencies thủ công:
bash
Copy code
sudo apt install ros-$ROS_DISTRO-hector-gazebo-plugins ros-$ROS_DISTRO-controller-man 
https://github.com/tu-darmstadt-ros-pkg/hector_quadrotor

sudo apt-get install ros-noetic-teleop-twist-keyboard

Khi mở Ubuntu, bạn chỉ cần chạy lần lượt các lệnh sau:

bash
Copy code
source ~/.bashrc
roscore
roslaunch hector_quadrotor_gazebo quadrotor_empty_world.launch
Nếu muốn điều khiển quadrotor:

bash
Copy code
rosrun teleop_twist_keyboard teleop_twist_keyboard.py
