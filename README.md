# test
import cv2
import os

video_path = r"G:\weding_photo\MVI_1408.MP4"
save_dir = r"G:\weding_photo\MVI_1408_frames_5"

os.makedirs(save_dir, exist_ok=True)

cap = cv2.VideoCapture(video_path)

if not cap.isOpened():
    raise RuntimeError("无法打开视频文件")

frame_id = 0
save_id = 0

while True:
    ret, frame = cap.read()
    if not ret:
        break

    if frame_id % 5 == 0:

        save_path = os.path.join(save_dir, f"frame_{frame_id:06d}.png")
        cv2.imwrite(save_path, frame)
        save_id += 1

    frame_id += 1

cap.release()
print(f"原始总帧数：{frame_id}")
print(f"实际保存帧数：{save_id}")
