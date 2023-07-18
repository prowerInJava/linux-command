# linux-command

import subprocess
import os

# 使用ffmpeg检测应用的响应
def check_app_response(file_path):
    """
    使用ffmpeg检测应用的响应
    :param file_path: 音频文件路径
    :return: None
    """
    command = f"ffprobe -v error -show_entries format=duration -of default=noprint_wrappers=1:nokey=1 {file_path}"
    response = subprocess.check_output(command, shell=True)
    print(f"应用的响应时间为: {response} 秒")

# 使用ffmpeg检测语音识别助手是否真的有tts播报
def check_tts_broadcast(file_path):
    """
    使用ffmpeg检测语音识别助手是否真的有tts播报
    :param file_path: 音频文件路径
    :return: None
    """
    command = f"ffprobe -v error -show_entries format=duration -of default=noprint_wrappers=1:nokey=1 {file_path}"
    response = subprocess.check_output(command, shell=True)
    if float(response) > 0:
        print("语音识别助手有tts播报")
    else:
        print("语音识别助手没有tts播报")


# 使用ffmpeg转换音频格式
def convert_audio_format(input_file, output_file):
    """
    使用ffmpeg转换音频格式
    :param input_file: 输入音频文件路径
    :param output_file: 输出音频文件路径
    :return: None
    """
    command = f"ffmpeg -i {input_file} {output_file}"
    subprocess.call(command, shell=True)
    print(f"音频文件已转换为: {output_file}")

# 使用ffmpeg提取音频中的音轨
def extract_audio_track(input_file, output_file):
    """
    使用ffmpeg提取音频中的音轨
    :param input_file: 输入音频文件路径
    :param output_file: 输出音频文件路径
    :return: None
    """
    command = f"ffmpeg -i {input_file} -map 0:a {output_file}"
    subprocess.call(command, shell=True)
    print(f"音轨已提取到: {output_file}")
# 使用ffmpeg提取视频中的音轨
def extract_video_track(input_file, output_file):
    """
    使用ffmpeg提取视频中的音轨
    :param input_file: 输入视频文件路径
    :param output_file: 输出音轨文件路径
    :return: None
    """
    command = f"ffmpeg -i {input_file} -map 0:v {output_file}"
    subprocess.call(command, shell=True)
    print(f"视频中的音轨已提取到: {output_file}")

# 使用ffmpeg转换视频格式
def convert_video_format(input_file, output_file):
    """
    使用ffmpeg转换视频格式
    :param input_file: 输入视频文件路径
    :param output_file: 输出视频文件路径
    :return: None
    """
    command = f"ffmpeg -i {input_file} {output_file}"
    subprocess.call(command, shell=True)
    print(f"视频文件已转换为: {output_file}")

# 使用ffmpeg检测视频的长度
def check_video_duration(file_path):
    """
    使用ffmpeg检测视频的长度
    :param file_path: 视频文件路径
    :return: None
    """
    command = f"ffprobe -v error -show_entries format=duration -of default=noprint_wrappers=1:nokey=1 {file_path}"
    response = subprocess.check_output(command, shell=True)
    print(f"视频的长度为: {response} 秒")
# 使用ffmpeg将视频处理为帧图片
def video_to_frames(input_file, output_folder):
    """
    使用ffmpeg将视频处理为帧图片
    :param input_file: 输入视频文件路径
    :param output_folder: 输出帧图片的文件夹路径
    :return: None
    """
    if not os.path.exists(output_folder):
        os.makedirs(output_folder)
    command = f"ffmpeg -i {input_file} {output_folder}/frame%03d.jpg"
    subprocess.call(command, shell=True)
    print(f"视频已处理为帧图片，存储在: {output_folder}")

# 使用ffmpeg将视频缩小暂用的存储空间
def reduce_video_size(input_file, output_file, bitrate="500k"):
    """
    使用ffmpeg将视频缩小暂用的存储空间
    :param input_file: 输入视频文件路径
    :param output_file: 输出视频文件路径
    :param bitrate: 视频比特率，默认为500k
    :return: None
    """
    command = f"ffmpeg -i {input_file} -b:v {bitrate} {output_file}"
    subprocess.call(command, shell=True)
    print(f"视频已缩小暂用的存储空间，新视频文件为: {output_file}")


