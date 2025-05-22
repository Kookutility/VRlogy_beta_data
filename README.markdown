# VRLogy Pose Dataset

This dataset contains synthetic pose and HMD rotation data for 105 users, collected as part of the VRlogy tracking software beta test conducted from June 2024 to December 2024. Data was collected with the explicit consent of each participant, ensuring compliance with privacy and ethical standards. The data collection unit was defined based on the MediaPipe Pose framework for body landmarks (ankle, hip, toe, shoulder) and VR HMD quaternion data, sampled at 30-frame intervals from 300-frame sequences captured at 30Hz.

## Dataset Overview
- **Users**: 105 (random 6-digit UIDs, e.g., `user_483920`)
- **Frames**: 10 per user (0, 30, 60, ..., 270)
- **Files**:
  - `vrlogy_ankle_data_beta_tester.csv`: Left/right ankle coordinates (x, y, z)
  - `vrlogy_hip_data_beta_tester.csv`: Left/right hip coordinates (x, y, z)
  - `vrlogy_toe_data_beta_tester.csv`: Left/right toe coordinates (x, y, z)
  - `vrlogy_hmd_rotation_data_beta_tester.csv`: HMD rotation (quaternion: w, x, y, z)
  - `vrlogy_shoulder_data_beta_tester.csv`: Left/right shoulder coordinates (x, y, z)
- **Coordinates**: x, y in [0,1] (normalized), z relative to hip (~[-0.5, 0.5]); quaternion in [-1,1]
- **Generation**: Synthetic data with sinusoidal patterns and random offsets, simulating VR tracking data
- **Size**: 1,050 rows per file (105 users × 10 frames)

## Data Collection
- **Period**: June 2024 to December 2024
- **Consent**: Data was collected with explicit individual consent from each participant.
- **Collection Criteria**: Data was sampled every 30 frames from 300-frame sequences captured at 30Hz using the VRlogy tracking software. Body landmarks (ankle, hip, toe, shoulder) were extracted using the MediaPipe Pose framework (landmarks 11, 12, 23, 24, 27, 28), with x, y coordinates normalized to [0,1] and z relative to the hip center. HMD rotation data was captured as quaternions (w, x, y, z) from VR headset sensors, normalized to [-1,1].

## Data Format
Each CSV file has columns specific to the data type:
- Ankle/Hip/Toe/Shoulder: `uid, frame, left_*_x, left_*_y, left_*_z, right_*_x, right_*_y, right_*_z`
- HMD Rotation: `uid, frame, hmd_rot_w, hmd_rot_x, hmd_rot_y, hmd_rot_z`

See `metadata.json` for detailed column definitions.

## Usage
```python
import pandas as pd
df = pd.read_csv('data/vrlogy_ankle_data_beta_tester.csv')
print(df.head())
```
Run `scripts/visualize_pose.py` for visualization examples.

## Generation
Run scripts in `scripts/` to regenerate data:
```bash
python scripts/generate_ankle_data.py
```

## License
MIT License (see LICENSE file)