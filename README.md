# BazelConversion
Pb file to Tflite file conversion using TOCO command line.

TOCO is a Tensorflow optimizing converter that can convert a TensorFlow GraphDef to TensorFlow Lite flatbuffer. We need to build TOCO with Bazel from Tensorflow repository and use it to convert the .pb file to a .tflite format.

The standard TensorFlow model obtained from our traind model cannot be used directly in TensorFlow Lite. We need to freeze the graph and convert the model to flatbuffer format (.tflite). There are two ways to convert the model: use TOCO command-line or python API (which uses TOCO under the hood).

You will need Linux or macOS for this step as TOCO is not available and cannot be bulit on Windows at the moment.

The steps involved using TOCO command-line are as follows:

1. Install Bazel :

   Install Bazel by following the instructions.

2. Clone TensorFlow repository :

        git clone https://github.com/tensorflow/tensorflow

3. Build TOCO : 
	Navigate to the TensorFlow repository directory, run the following command to build TOCO.
	
        bazel build tensorflow/contrib/lite/toco:toco
	
4. Convert model :

    Stay at the TensorFlow repository directory, run the following command to convert the model.
          /bazel-bin/tensorflow/contrib/lite/toco/toco  \
        --input_file=./saved_model/mnist.pb \
        --input_format=TENSORFLOW_GRAPHDEF  --output_format=TFLITE \
        --output_file=./mnist.tflite --inference_type=FLOAT \
        --input_type=FLOAT --input_arrays=x \
        --output_arrays=output --input_shapes=1,28,28,1


The input_file argument should point to the TensorFlow GraphDef file (.pb file). The output_file argument specifies the location for the converted model.The input_shapes is the shape of the input image used in the model.



