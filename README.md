# MapZoo: A Collection of 1:10-Scale Racing Maps

A curated collection of 1:10-scale 2D racing maps with centerlines, optimized racing lines, speed-scaling settings, and overtaking-sector annotations.

This dataset is designed for autonomous racing, trajectory planning, simulation, path tracking, overtaking evaluation, and reinforcement-learning environment development.

> The current dataset contains **32** tracks/maps with a total size of approximately **230 MB**. The data is stored mainly in `PNG`, `YAML`, `CSV`, and `JSON` formats, making it easy to use with Python, ROS-style map pipelines, Roboracer/f110-like environments, and custom simulators.

The following overview visualizes all included tracks with their occupancy maps, centerlines, optimized racing lines, and reconstructed track boundaries.

![Track overview](all_tracks_overview.png)

---

## Highlights

- **32 tracks**: a diverse set of benchmark-ready tracks.
- **Occupancy-grid map format**: each map provides `.png` and `.yaml` files compatible with common robotics map pipelines.
- **Centerline and racing line**: each track includes sampled centerline and optimized racing-line CSV files.
- **Simulation-ready metadata**: speed-scaling sectors and overtaking-sector flags are provided per map.
- **Open and extensible structure**: adding new maps only requires following the same folder/file convention.
- **Race Stack compatible**: The dataset is designed to align seamlessly with the map format required by [ForzaETH Race Stack](https://github.com/ForzaETH/race_stack), making it easy to plug tracks into existing autonomous racing pipelines.

Last but not least, a ⭐ would be greatly appreciated and would serve as strong encouragement for my continued open-source research efforts : )

---

## Repository Structure

Each track is stored in an independent directory:

```text
<track_name>/
├── <track_name>.png                 # Occupancy-grid map image
├── <track_name>.yaml                # Map metadata for <track_name>.png
├── <track_name>-cent.png            # Centerline-oriented map image
├── <track_name>-cent.yaml           # Map metadata for <track_name>-cent.png
├── <track_name>_centerline.csv      # Sampled track centerline
├── <track_name>_racing_line.csv     # Optimized racing line
├── global_waypoints.json            # Global waypoints, trajectories, markers, lap-time metadata
├── speed_scaling.yaml               # Speed-scaling sectors
└── ot_sectors.yaml                  # Overtaking-sector configuration
```

Example:

```text
Austin/
├── Austin.png
├── Austin.yaml
├── Austin-cent.png
├── Austin-cent.yaml
├── Austin_centerline.csv
├── Austin_racing_line.csv
├── global_waypoints.json
├── speed_scaling.yaml
└── ot_sectors.yaml
```

---

## Included Tracks

| Track         | Centerline Points | Racing-line Points | Racing-line Length (m) | Est. Lap Time (s) |
| ------------- | ----------------: | -----------------: | ---------------------: | ----------------: |
| Austin        |              1552 |               1436 |                  143.5 |             20.54 |
| BrandsHatch   |              2086 |               2023 |                  202.1 |             23.86 |
| Budapest      |              1744 |               1643 |                  164.2 |             21.58 |
| Catalunya     |              2098 |               2013 |                  201.1 |             25.12 |
| IMS           |              1413 |               1393 |                  139.1 |             13.42 |
| Melbourne     |              1480 |               1412 |                  141.1 |             16.86 |
| MexicoCity    |              1488 |               1418 |                  141.7 |             16.62 |
| Montreal      |              1269 |               1225 |                  122.3 |             13.54 |
| Monza         |              1360 |               1317 |                  131.6 |             14.13 |
| MoscowRaceway |              1704 |               1590 |                  158.9 |             21.45 |
| Norisring     |              1443 |               1407 |                  140.5 |             14.46 |
| Nuerburgring  |              1885 |               1816 |                  181.5 |             22.14 |
| Oschersleben  |              1838 |               1762 |                  176.1 |             22.09 |
| Sakhir        |              2306 |               2236 |                  223.4 |             26.58 |
| SaoPaulo      |              2119 |               2024 |                  202.3 |             24.18 |
| Sepang        |              2435 |               2347 |                  234.6 |             28.92 |
| Shanghai      |              2261 |               2151 |                  215.0 |             26.82 |
| Silverstone   |              1766 |               1701 |                  170.0 |             21.06 |
| Sochi         |              1427 |               1355 |                  135.3 |             17.31 |
| Spa           |              1722 |               1648 |                  164.7 |             19.99 |
| Spielberg     |              1738 |               1667 |                  166.6 |             20.21 |
| YasMarina     |              1682 |               1587 |                  158.6 |             20.80 |
| Zandvoort     |              2244 |               2155 |                  215.3 |             26.17 |
| berlin        |              1359 |               1292 |                  129.1 |             15.76 |
| f             |              1723 |               1640 |                  163.8 |             19.32 |
| hangar        |              1411 |               1355 |                  135.4 |             16.22 |
| mtl           |              1552 |               1506 |                  150.4 |             16.77 |
| overtake_map  |              1093 |               1051 |                  104.9 |             12.26 |
| torino        |              1369 |               1311 |                  130.9 |             15.80 |
| warehouse_v0  |              1823 |               1767 |                  176.5 |             21.14 |
| warehouse_v1  |              1469 |               1419 |                  141.8 |             17.59 |
| warehouse_v2  |              1649 |               1576 |                  157.5 |             19.60 |

---

## 🛠️ File Format

### 1. Map YAML

`<track_name>.yaml` and `<track_name>-cent.yaml` describe the corresponding PNG map.

Typical fields:

```yaml
image: Austin.png
resolution: 0.1
origin: [-4.0, -10.0, 0]
negate: 0
occupied_thresh: 0.65
free_thresh: 0.196
```

Field meaning:

| Field             | Meaning                                        |
| ----------------- | ---------------------------------------------- |
| `image`           | Relative path to the map image                 |
| `resolution`      | Map resolution in meters per pixel             |
| `origin`          | World-frame origin of the map `[x, y, yaw]`    |
| `negate`          | Whether to invert the occupancy interpretation |
| `occupied_thresh` | Occupancy threshold                            |
| `free_thresh`     | Free-space threshold                           |

---

### 2. Centerline and Racing-line CSV

`<track_name>_centerline.csv` and `<track_name>_racing_line.csv` use semicolon-separated columns:

```text
id; s_m; d_m; x_m; y_m; d_right; d_left; psi_rad; kappa_radpm; vx_mps; ax_mps2
```

| Column        | Meaning                                                      |
| ------------- | ------------------------------------------------------------ |
| `id`          | Waypoint index                                               |
| `s_m`         | Arc length along the path, in meters                         |
| `d_m`         | Lateral offset, in meters                                    |
| `x_m`         | Waypoint x coordinate in map/world frame                     |
| `y_m`         | Waypoint y coordinate in map/world frame                     |
| `d_right`     | Distance to right track boundary                             |
| `d_left`      | Distance to left track boundary                              |
| `psi_rad`     | Heading angle in radians                                     |
| `kappa_radpm` | Curvature in radians per meter                               |
| `vx_mps`      | Reference velocity in meters per second                      |
| `ax_mps2`     | Reference longitudinal acceleration in meters per second squared |

Notes:

- Centerline files usually contain zero velocity and acceleration fields.
- Racing-line files contain optimized velocity and acceleration profiles.
- The sampling interval is approximately `0.1 m`, but exact spacing may vary slightly between tracks and optimized trajectories.

---

### 3. Global Waypoints JSON

`global_waypoints.json` stores richer trajectory and visualization data.

Top-level keys include:

```text
map_info_str
est_lap_time
centerline_markers
centerline_waypoints
global_traj_markers_iqp
global_traj_wpnts_iqp
global_traj_markers_sp
global_traj_wpnts_sp
trackbounds_markers
```

Important entries:

| Key                     | Meaning                                                      |
| ----------------------- | ------------------------------------------------------------ |
| `map_info_str`          | Text summary of estimated lap time and maximum speed         |
| `est_lap_time`          | Estimated lap time, usually corresponding to the SP trajectory |
| `centerline_waypoints`  | Centerline waypoint list                                     |
| `global_traj_wpnts_iqp` | IQP optimized global trajectory waypoints                    |
| `global_traj_wpnts_sp`  | SP optimized global trajectory waypoints                     |
| `*_markers`             | Visualization markers, useful for ROS/RViz-style visualization |
| `trackbounds_markers`   | Track boundary visualization markers                         |

The waypoint structure is consistent with the CSV fields:

```json
{
  "id": 0,
  "s_m": 0.0,
  "d_m": 0.0,
  "x_m": 23.18,
  "y_m": -3.13,
  "d_right": 2.56,
  "d_left": 0.64,
  "psi_rad": 0.49,
  "kappa_radpm": 0.37,
  "vx_mps": 5.31,
  "ax_mps2": -1.13
}
```

---

### 4. Speed Scaling

`speed_scaling.yaml` defines track sectors where the reference speed can be scaled.

Example:

```yaml
global_limit: 0.7
n_sectors: 1
Sector0:
  start: 0
  end: 1436
  scaling: 0.7
  only_FTG: false
  no_FTG: true
```

| Field             | Meaning                                                     |
| ----------------- | ----------------------------------------------------------- |
| `global_limit`    | Global speed-scaling limit                                  |
| `n_sectors`       | Number of speed-scaling sectors                             |
| `SectorX.start`   | Start waypoint index                                        |
| `SectorX.end`     | End waypoint index                                          |
| `SectorX.scaling` | Speed scaling factor in this sector                         |
| `only_FTG`        | Whether the sector is only for Follow-the-Gap style driving |
| `no_FTG`          | Whether Follow-the-Gap is disabled in this sector           |

---

### 5. Overtaking Sectors

`ot_sectors.yaml` defines areas where overtaking behavior is enabled.

Example:

```yaml
n_sectors: 1
yeet_factor: 1.25
spline_len: 30
ot_sector_begin: 0.5
Overtaking_sector0:
  start: 0
  end: 1436
  ot_flag: true
```

| Field                      | Meaning                                                      |
| -------------------------- | ------------------------------------------------------------ |
| `n_sectors`                | Number of overtaking sectors                                 |
| `yeet_factor`              | Lateral/overtaking aggressiveness factor used by some planners |
| `spline_len`               | Spline length parameter for local overtaking trajectory generation |
| `ot_sector_begin`          | Relative or normalized beginning threshold for overtaking logic |
| `Overtaking_sectorX.start` | Start waypoint index                                         |
| `Overtaking_sectorX.end`   | End waypoint index                                           |
| `ot_flag`                  | Whether overtaking is enabled in this sector                 |

---

## 🪄 Quick Start

### 1. Clone the Repository

```bash
git clone git@github.com:zhouhengli/MapZoo.git
cd MapZoo
```

### 2. Install Minimal Python Dependencies

For reading and visualizing the data:

```bash
pip install numpy pandas pyyaml matplotlib pillow
```

### 3. Load a Map YAML

```python
from pathlib import Path
import yaml

track_dir = Path("Austin")

with open(track_dir / "Austin.yaml", "r") as f:
    map_cfg = yaml.safe_load(f)

print(map_cfg)
```

### 4. Load a Racing Line

```python
from pathlib import Path
import pandas as pd

track_dir = Path("Austin")
racing_line = pd.read_csv(track_dir / "Austin_racing_line.csv", sep=";", skipinitialspace=True)

print(racing_line.head())
print(racing_line.columns.tolist())
```

### 5. Load Global Waypoints

```python
from pathlib import Path
import json

track_dir = Path("Austin")

with open(track_dir / "global_waypoints.json", "r") as f:
    global_waypoints = json.load(f)

sp_waypoints = global_waypoints["global_traj_wpnts_sp"]["wpnts"]
iqp_waypoints = global_waypoints["global_traj_wpnts_iqp"]["wpnts"]

print("SP waypoint count:", len(sp_waypoints))
print("IQP waypoint count:", len(iqp_waypoints))
print("Estimated lap time:", global_waypoints["est_lap_time"]["data"])
```

### 6. Plot Centerline and Racing Line

```python
from pathlib import Path
import pandas as pd
import matplotlib.pyplot as plt

track = "Austin"
track_dir = Path(track)

centerline = pd.read_csv(track_dir / f"{track}_centerline.csv", sep=";", skipinitialspace=True)
racing_line = pd.read_csv(track_dir / f"{track}_racing_line.csv", sep=";", skipinitialspace=True)

plt.figure(figsize=(8, 8))
plt.plot(centerline["x_m"], centerline["y_m"], label="Centerline")
plt.plot(racing_line["x_m"], racing_line["y_m"], label="Racing line")
plt.axis("equal")
plt.xlabel("x [m]")
plt.ylabel("y [m]")
plt.legend()
plt.title(track)
plt.show()
```

---

## Typical Use Cases

This dataset can be used for:

- Autonomous racing simulation
- Roboracer /  f110-style planning experiments
- Global trajectory tracking
- Local planner benchmarking
- Multi-agent racing and competitive driving
- Overtaking-policy development
- Reinforcement learning environment construction
- Trajectory optimization and speed-profile analysis
- Map-based localization and path-following experiments

---

## Naming Convention

When adding a new track, use the following naming convention:

```text
<track_name>/
├── <track_name>.png
├── <track_name>.yaml
├── <track_name>-cent.png
├── <track_name>-cent.yaml
├── <track_name>_centerline.csv
├── <track_name>_racing_line.csv
├── global_waypoints.json
├── speed_scaling.yaml
└── ot_sectors.yaml
```

Recommendations:

- Keep the directory name and file prefix consistent.
- Use semicolon-separated CSV files to stay compatible with the existing data.
- Keep waypoint fields consistent with the existing schema.
- Keep map resolution and origin explicitly defined in YAML.
- Validate that the racing line stays within the left/right track boundaries.

---

## Data Validation Checklist

Before submitting a new map or modifying an existing one, check that:

- [ ] The map PNG can be loaded successfully.
- [ ] The YAML `image` field points to the correct PNG file.
- [ ] `resolution`, `origin`, `occupied_thresh`, and `free_thresh` are defined.
- [ ] Centerline and racing-line CSV files contain all required columns.
- [ ] CSV files use `;` as the separator.
- [ ] `global_waypoints.json` contains centerline, IQP/SP trajectory, and track-bound entries.
- [ ] `speed_scaling.yaml` sector indices are within the waypoint range.
- [ ] `ot_sectors.yaml` sector indices are within the waypoint range.
- [ ] The racing line and centerline are visually checked on the map.

---

## Known Notes

- The repository currently contains map/trajectory data only. Planner, controller, simulator, or training code should be provided separately if needed.
- Lap-time values in `global_waypoints.json` are estimated values from trajectory-generation metadata, not guaranteed real-world lap times.
- Track names are kept as originally stored. Some names are lowercase or abbreviated, such as `berlin`, `f`,  `mtl`, and `overtake_map`.
- CSV values are floating-point data; small numerical differences may occur if files are regenerated by another optimization pipeline.

---

## Contributing

Contributions are welcome. Suggested contribution types:

- Add new track maps.
- Improve or regenerate centerlines and racing lines.
- Add validation scripts.
- Add visualization examples.
- Add simulator-specific loading adapters.
- Fix inconsistent metadata or map naming.

For each new track, please include the full set of map, YAML, CSV, JSON, speed-scaling, and overtaking-sector files.

---

## Contact

Please contact [Zhouheng Li](https://zhouhengli.github.io/) if you have any questions or suggestions. If you encounter any issues or have questions during deployment, feel free to open an issue or submit a pull request—contributions and feedback are very welcome.

---

## 📑 Citation

If you use this dataset in academic work, please cite this repository.

```
TBD
```

