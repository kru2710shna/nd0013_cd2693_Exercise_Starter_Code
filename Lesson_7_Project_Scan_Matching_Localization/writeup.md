# 🚗 Scan-Matching-Based Vehicle Localization  

## 📝 Project Summary  
This project focuses on estimating the location of a simulated car as it moves at least 170 meters without exceeding a pose error of 1.2 meters. The car operates in a virtual environment and uses a LiDAR sensor to capture regular scans of its surroundings. A pre-generated map (`map.pcd`) serves as a reference, and by matching the incoming LiDAR scans with this map, the vehicle's pose can be continuously estimated. The map itself is sourced from the [CARLA simulator](https://carla.org/).

---

## 🧩 Implementation Breakdown  

### 🔹 Step 1: Point Cloud Preprocessing  
Begin by applying a **voxel grid filter** to downsample the incoming LiDAR scan. Work with `cloudFiltered` and `scanCloud` to reduce the scan density, making subsequent registration faster and more efficient.

---

### 🔹 Step 2: Pose Estimation with ICP or NDT  
This is the core of the system. Utilize **Iterative Closest Point (ICP)** or **Normal Distributions Transform (NDT)** to compute the transformation matrix that best aligns the filtered scan with the map. This transformation represents the car's estimated motion.

---

### 🔹 Step 3: Scan Transformation and Visualization  
After calculating the optimal pose, apply the transformation to the filtered scan to align it with the world (ego) coordinate frame. Replace `scanCloud` with this updated cloud when calling `renderPointCloud`, so that the aligned scan is visualized.

---

## ▶️ How to Run  

### 1️⃣ Compile the Project (Terminal Tab 1)
```bash
cd /home/workspace/c3-project
cmake .
make
```

## Start the CARLA Simulator (Terminal Tab 2)
```bash
su - student
cd /home/workspace
./run-carla.sh
```

## Run the Scan Matching Program (Terminal Tab 1)
```bash
cd /home/workspace

# Run with NDT
./cloud_loc

# Run with ICP
./cloud_loc 2

```

## Output Preview

Demonstration of vehicle localization using LiDAR scan matching and ICP
Final pose alignment shown through corrected point cloud rendering

![ICPTouchDown](https://github.com/user-attachments/assets/e23d4c71-140e-492b-a4fe-a0ac132df9e2)


