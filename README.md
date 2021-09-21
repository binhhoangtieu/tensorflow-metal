Chia sẻ với bạn nào cài tensorflow with GPU trên máy Macbook Pro M1

Sau vài ngày loay hoay cài tensorflow trên Macbook có hỗ trợ GPU không được, chỉ chạy tensorflow without GPU, mình đã thử cách này, chia sẻ với ai quan tâm:

Trước tiên cần cài Xcode, bộ công cụ đầy đủ cho lập trình trên nền MacOS, cái này vào App Store để cài, bộ cài khá lớn >11 Gb nên mất khá nhiều thời gian. Hoặc có thể vào Terminal, chạy lệnh: xcode-select --install để cài mỗi bộ công cụ dòng lệnh. Sau đó thực hiện các bước sau:

B1: Cài conda trên môi trường Miniforge3 trước, download miniforge3 ở đây: https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-MacOSX-arm64.sh

B2: Mở Terminal, vào thư mục vừa download, chạy lệnh: sh ./Miniforge3-MacOSX-arm64.sh

B3: Kích hoạt môi trường miniforge, dùng lệnh source ./miniforge3/bin/activate

B4: Download file tensorflow-apple-metal.yml của Jeffheaton vào thư mục hiện thời, link: https://raw.githubusercontent.com/jeffheaton/t81_558_deep_learning/master/tensorflow-apple-metal.yml Sau đó chạy lệnh trong Terminal:

export GRPC_PYTHON_BUILD_SYSTEM_OPENSSL=1

export GRPC_PYTHON_BUILD_SYSTEM_ZLIB=1

conda env create -f tensorflow-apple-metal.yml -n tf_metal

#(tf_metal là tên môi trường ảo, bạn có thể đặt bất kỳ).

Như vậy bạn đã hoàn thành cài đặt tensorflow-metal và các dependencies packages. Để kích hoạt môi trường ảo vừa tạo, chạy lệnh: conda activate tf_metal Lúc này môi trường ảo đã kích hoạt, ta có thể vào python và sử dụng Tensorflow with GPU.

Để test xem GPU có hoạt động không, ta dùng đoạn code sau (nguồn: Github JeffHeaton):

import sys import tensorflow.keras import pandas as pd import sklearn as sk import tensorflow as tf

print(f"Tensor Flow Version: {tf.version}")

print(f"Keras Version: {tensorflow.keras.version}")

print()

print(f"Python {sys.version}")

print(f"Pandas {pd.version}")

print(f"Scikit-Learn {sk.version}")

gpu = len(tf.config.list_physical_devices('GPU'))>0

print("GPU is", "available" if gpu else "NOT AVAILABLE")

Nếu kết quả là:

Tensor Flow Version: 2.5.0

Keras Version: 2.5.0

Python 3.9.7 | packaged by conda-forge | (default, Sep 14 2021, 01:14:24) [Clang 11.1.0 ]

Pandas 1.3.3

Scikit-Learn 0.24.2

GPU is available

thì bạn đã thành công! Chúc may mắn

PS: Hình sau nói lên tất cả, hiệu năng của M1 quá ấn tượng (nguồn tensorflow.org)
