# Introduction
E3PO is an **O**pen **P**latform for **3**60° video streaming simulation and **E**valuation. E3PO is designed to support the simulation of a variety of 360° video streaming approaches that have been proposed so far, including projection based, tile based, or transcoding based. Particularly, E3PO allows users to convert 360° video into standard or customized projections, segment video into equal or adaptive sizes, implement customized motion prediction algorithms, apply different streaming strategies, and evaluate using any user-specific metrics. Most importantly, E3PO generates the actual visual sequences that will display on the user screen for each simulation. 

Therefore, E3PO provides a perfect solution to objectively compare the performance of different 360° video streaming approaches, using the same video content and same motion trace.



# Framework
The framework of E3PO is illustrated as the following figure, which consists of three principal modules, i.e., the ***video pre-processor***, the ***streaming simulator*** and the ***system evaluator***.

To simulate a streaming approach, the ***video pre-processor*** first segments the 360° panoramic video into small video tile chunks according to users’ specific projection and tiling parameters. Then the ***streaming simulator*** reads the provided head motion trace, and simulates the detailed streaming actions which include when and which video chunk is transmitted. Last, the ***system evaluator*** synthesizes the video sequence that is displayed on the user screen and calculates various metrics.

![](/docs/Framework.jpg "e3po_framework")

# Proposed method
The proposed method focuses on fine-tuning the video encoder parameters to optimize the encoding process within the framework. The detailed description of the modified method.

Utilization of Constant Rate Factor (CRF): In our proposed method, instead of directly specifying the QP values for encoding, the modified method employs the Constant Rate Factor (CRF) approach. CRF dynamically adjusts the compression
level based on the desired output quality, ensuring consistent visual quality across encoded videos while optimizing file size. By utilizing CRF, the encoding process becomes more adaptive and efficient, resulting in improved compression performance and enhanced video quality.

Optimized Encoding Command: The encode_dst_video function constructs an optimized ffmpeg command tailored to the chosen encoding settings. This command is designed to maximize encoding performance and resource utilization, thereby improving overall efficiency and quality of the encoding process. By optimizing the encoding command, the modified method ensures optimal utilization of hardware resources and delivers better compression quality with reduced file sizes.

Support for Encoding Parameters: Our proposed method expands the capability of the encoder to accommodate a broader range of encoding parameters. These parameters include the type of encoder, preset settings, Group of Pictures (GOP) size, and the Quality Parameter (QP) list. This enhancement provides users with more flexibility and control over the encoding process, allowing them to tailor it according to specific streaming requirements and preferences.

# Experimental Setup
In our proposed methods, we use the following setting parameters for the encoder, specifically focusing on the Constant Rate Factor (CRF) method.

○ encoder: Specifies the video encoder to be used. In this case, it defaults to libx264, which is a widely used H.264 encoder.

○ preset: Defines the encoding preset, which determines the trade-off between encoding speed and compression efficiency. The default value is slow for better compression efficiency,( indicating a slower encoding process that typically results in better compression.

○ gop: Sets the Group of Pictures (GOP) size. GOP is a sequence of consecutive frames that starts with a keyframe. A smaller GOP size can improve video quality but may increase file size.

○ qp: Stands for Quantization Parameter. It's a value used in quantization, which determines the level of compression applied to each frame. Lower values result in better quality but larger file sizes.

Here, qp_list is a list of quantization parameters, and [0] is used to get the first value from the list, which is then assigned to qp.
The ffmpeg command used for encoding the destination video is updated to include CRF encoding parameters.The -crf option is added to specify the CRF value obtained from the qp_list. In our proposed method, it utilizes CRF dynamically, allowing it to adjust the compression level based on the desired output quality automatically. By using CRF, you can achieve better control over video quality without specifying a fixed bitrate, resulting in more efficient compression and improved resolution.

Discussion about the Proposed Method Result and Limitations:

While the proposed method offers several advantages over the original framework, it's essential to consider potential limitations and areas for further improvement.

Some points for discussion include:

1. Parameter Sensitivity: Despite the benefits of CRF and optimized encoding
parameters, the effectiveness of the proposed method may depend on the
careful tuning of these parameters. Fine-tuning CRF values and other
encoding settings may be necessary to achieve the desired balance between
compression and quality for different streaming scenarios.

3. Hardware Dependency: The performance of the proposed method may vary
depending on the hardware capabilities and resource constraints of the
streaming environment. Compatibility testing and optimization efforts are
required to ensure consistent performance across different hardware
configurations and platforms.

There is always room for improvement.
