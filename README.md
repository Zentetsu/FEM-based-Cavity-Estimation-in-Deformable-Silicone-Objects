# Dataset: FEM-based Cavity Estimation in Deformable Silicone Objects

## Overview

This dataset contains robotic indentation measurements collected on silicone cube specimens with internal cavities of varying geometry. It supports the results reported in:

> Morant T., Cordero-Alvarado M., Yang T., Kurosawa K., Tanizaki Y., Nagano N., Yu W. *FEM-based estimation-correction with Minimal Indentation Set for Internal Cavity Classification and Geometry Estimation in Deformable Objects.* MDPI Sensors, Special Issue "Flexible Sensing in Robotics, Healthcare, and Beyond."

---

## Experimental Setup

Silicone cubes (Dragon Skin 10, 50 mm side, E = 0.25 MPa, ν = 0.49) were indented using a parallel-jaw gripper at maximum force F_MAX = 7.5 N. Two jaw widths were tested:

| Gripper | Jaw width | Files prefix |
|---------|-----------|--------------|
| G25     | 25 mm     | `*_G25.*`    |
| G20     | 20 mm     | `*_G20.*`    |

### Cavity types

The dataset codes map to the paper's notation as follows:

| Code | Paper notation | Cavity geometry | Dimensions | Origin (x,y,z) mm |
|------|---------------|----------------|------------|-------------------|
| M0   | M_full        | None (homogeneous) | — | — |
| M1   | M_sphere      | Sphere | r = 20 mm | (0,0,0) |
| M2R  | M_cuboid      | Rectangular box | 40 × 40 × 30 mm | (0,0,0) |
| M2S  | M_cube        | Cubic box | 40 × 40 × 40 mm | (0,0,0) |
| M3   | M_pyramid     | Pyramid, apex along +Y | base 40 × 40 mm, h = 40 mm | (0,0,−20) |

The baseline types B0–B3 in `baseline_force_deformation_G{XX}.csv` are homogeneous reference measurements corresponding to each cavity type: B0 for M_full, B1 for M_sphere, B2R for M_cuboid, B2S for M_cube, and B3 for M_pyramid. These are used exclusively for Minimal Indentation Set selection.

### Indentation locations

54 points per face configuration, in three categories: **center** (6 points, ±X/Y/Z face centers), **edge** (24 points), and **off** (24 points). The full ordered list is in `indentation_points.txt`.

The coordinate origin is at the cube center. Face normals point inward.

---

## Files

### `indentation_depths_G{XX}.csv`

| Column | Unit | Description |
|--------|------|-------------|
| `indentation_point` | — | Point name |
| `cavity_type` | — | M0, M1, M2R, M2S, or M3 |
| `depth_meas_mm` | mm | Measured indentation depth |
| `depth_base_mm` | mm | Baseline depth (M0, same point) |

### `forces_G{XX}.csv`

| Column | Unit | Description |
|--------|------|-------------|
| `indentation_point` | — | Point name |
| `cavity_type` | — | M0, M1, M2R, M2S, or M3 |
| `indentation_set` | — | `center`, `center_edge`, or `center_off` |
| `force_meas_N` | N | Measured reaction force |
| `force_base_N` | N | Baseline force (M0, same point and set) |

Empty entries indicate measurements not collected for that combination.

### `baseline_force_deformation_G{XX}.csv`

Force and surface deformation on homogeneous baseline cubes, used for Minimal Indentation Set selection. B0–B3 correspond to distinct baseline specimens or conditions.

| Column | Unit | Description |
|--------|------|-------------|
| `indentation_point` | — | Point name |
| `baseline_type` | — | B0, B1, B2R, B2S, or B3 |
| `force_N` | N | Reaction force at terminal depth |
| `deformation_mm` | mm | Maximum surface deformation |

### `indentation_points.txt`

Ordered list of the 54 indentation point names matching the positional index used in all CSV files.
