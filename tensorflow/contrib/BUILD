# Description:
#   contains parts of TensorFlow that are experimental or unstable and which are not supported.

licenses(["notice"])  # Apache 2.0

package(default_visibility = ["//tensorflow:__subpackages__"])

load("//third_party/mpi:mpi.bzl", "if_mpi")
load("@local_config_cuda//cuda:build_defs.bzl", "if_cuda")
load("//tensorflow:tensorflow.bzl", "if_not_windows")
load("//tensorflow:tensorflow.bzl", "if_not_windows_cuda")

py_library(
    name = "contrib_py",
    srcs = glob(
        ["**/*.py"],
        exclude = [
            "**/*_test.py",
        ],
    ),
    srcs_version = "PY2AND3",
    visibility = ["//visibility:public"],
    deps = [
        "//tensorflow/contrib/all_reduce",
        "//tensorflow/contrib/batching:batch_py",
        "//tensorflow/contrib/bayesflow:bayesflow_py",
        "//tensorflow/contrib/boosted_trees:init_py",
        "//tensorflow/contrib/checkpoint/python:checkpoint",
        "//tensorflow/contrib/cluster_resolver:cluster_resolver_py",
        "//tensorflow/contrib/coder:coder_py",
        "//tensorflow/contrib/compiler:compiler_py",
        "//tensorflow/contrib/autograph",
        "//tensorflow/contrib/constrained_optimization",
        "//tensorflow/contrib/copy_graph:copy_graph_py",
        "//tensorflow/contrib/crf:crf_py",
        "//tensorflow/contrib/cudnn_rnn:cudnn_rnn_py",
        "//tensorflow/contrib/data",
        "//tensorflow/contrib/deprecated:deprecated_py",
        "//tensorflow/contrib/distribute:distribute",
        "//tensorflow/contrib/distributions:distributions_py",
        "//tensorflow/contrib/eager/python:tfe",
        "//tensorflow/contrib/estimator:estimator_py",
        "//tensorflow/contrib/factorization:factorization_py",
        "//tensorflow/contrib/feature_column:feature_column_py",
        "//tensorflow/contrib/framework:framework_py",
        "//tensorflow/contrib/gan",
        "//tensorflow/contrib/graph_editor:graph_editor_py",
        "//tensorflow/contrib/grid_rnn:grid_rnn_py",
        "//tensorflow/contrib/hooks",
        "//tensorflow/contrib/image:distort_image_py",
        "//tensorflow/contrib/image:image_py",
        "//tensorflow/contrib/image:single_image_random_dot_stereograms_py",
        "//tensorflow/contrib/input_pipeline:input_pipeline_py",
        "//tensorflow/contrib/integrate:integrate_py",
        "//tensorflow/contrib/keras",
        "//tensorflow/contrib/kernel_methods",
        "//tensorflow/contrib/kfac",
        "//tensorflow/contrib/labeled_tensor",
        "//tensorflow/contrib/layers:layers_py",
        "//tensorflow/contrib/learn",
        "//tensorflow/contrib/legacy_seq2seq:seq2seq_py",
        "//tensorflow/contrib/libsvm",
        "//tensorflow/contrib/linalg:linalg_py",
        "//tensorflow/contrib/linear_optimizer:sdca_estimator_py",
        "//tensorflow/contrib/linear_optimizer:sdca_ops_py",
        "//tensorflow/contrib/lookup:lookup_py",
        "//tensorflow/contrib/losses:losses_py",
        "//tensorflow/contrib/losses:metric_learning_py",
        "//tensorflow/contrib/memory_stats:memory_stats_py",
        "//tensorflow/contrib/meta_graph_transform",
        "//tensorflow/contrib/metrics:metrics_py",
        "//tensorflow/contrib/mixed_precision:mixed_precision",
        "//tensorflow/contrib/model_pruning",
        "//tensorflow/contrib/nccl:nccl_py",
        "//tensorflow/contrib/nearest_neighbor:nearest_neighbor_py",
        "//tensorflow/contrib/nn:nn_py",
        "//tensorflow/contrib/opt:opt_py",
        "//tensorflow/contrib/optimizer_v2:optimizer_v2_py",
        "//tensorflow/contrib/periodic_resample:init_py",
        "//tensorflow/contrib/predictor",
        "//tensorflow/contrib/proto",
        "//tensorflow/contrib/quantization:quantization_py",
        "//tensorflow/contrib/quantize:quantize_graph",
        "//tensorflow/contrib/receptive_field:receptive_field_py",
        "//tensorflow/contrib/recurrent:recurrent_py",
        "//tensorflow/contrib/reduce_slice_ops:reduce_slice_ops_py",
        "//tensorflow/contrib/remote_fused_graph/pylib:remote_fused_graph_ops_py",
        "//tensorflow/contrib/resampler:resampler_py",
        "//tensorflow/contrib/rnn:rnn_py",
        "//tensorflow/contrib/rpc",
        "//tensorflow/contrib/saved_model:saved_model_py",
        "//tensorflow/contrib/seq2seq:seq2seq_py",
        "//tensorflow/contrib/signal:signal_py",
        "//tensorflow/contrib/slim",
        "//tensorflow/contrib/slim:nets",
        "//tensorflow/contrib/solvers:solvers_py",
        "//tensorflow/contrib/sparsemax:sparsemax_py",
        "//tensorflow/contrib/specs",
        "//tensorflow/contrib/staging",
        "//tensorflow/contrib/stat_summarizer:stat_summarizer_py",
        "//tensorflow/contrib/stateless",
        "//tensorflow/contrib/summary:summary",
        "//tensorflow/contrib/tensor_forest:init_py",
        "//tensorflow/contrib/tensorboard",
        "//tensorflow/contrib/tensorrt:init_py",
        "//tensorflow/contrib/testing:testing_py",
        "//tensorflow/contrib/text:text_py",
        "//tensorflow/contrib/tfprof",
        "//tensorflow/contrib/timeseries",
        "//tensorflow/contrib/tpu",
        "//tensorflow/contrib/tpu:tpu_py",
        "//tensorflow/contrib/training:training_py",
        "//tensorflow/contrib/util:util_py",
        "//tensorflow/python:util",
        "//tensorflow/python/estimator:estimator_py",
    ] + if_mpi(["//tensorflow/contrib/mpi_collectives:mpi_collectives_py"]) + select({
        "//tensorflow:with_kafka_support_windows_override": [],
        "//tensorflow:with_kafka_support": [
            "//tensorflow/contrib/kafka",
        ],
        "//conditions:default": [],
    }) + select({
        "//tensorflow:with_aws_support_windows_override": [],
        "//tensorflow:with_aws_support": [
            "//tensorflow/contrib/kinesis",
        ],
        "//conditions:default": [],
    }) + if_not_windows_cuda([
        "//tensorflow/contrib/fused_conv:fused_conv_py",  # unresolved symbols, need to export more symbols
    ]) + if_not_windows([
        "//tensorflow/contrib/bigtable",  # depends on bigtable
        "//tensorflow/contrib/cloud:cloud_py",  # doesn't compile on Windows
        "//tensorflow/contrib/ffmpeg:ffmpeg_ops_py",
        "//tensorflow/contrib/lite/python:lite",  # unix dependency, need to fix code
    ]),
)

cc_library(
    name = "contrib_kernels",
    visibility = ["//visibility:public"],
    deps = [
        "//tensorflow/contrib/boosted_trees:boosted_trees_kernels",
        "//tensorflow/contrib/coder:all_kernels",
        "//tensorflow/contrib/data/kernels:dataset_kernels",
        "//tensorflow/contrib/factorization/kernels:all_kernels",
        "//tensorflow/contrib/input_pipeline:input_pipeline_ops_kernels",
        "//tensorflow/contrib/layers:sparse_feature_cross_op_kernel",
        "//tensorflow/contrib/nearest_neighbor:nearest_neighbor_ops_kernels",
        "//tensorflow/contrib/rnn:all_kernels",
        "//tensorflow/contrib/seq2seq:beam_search_ops_kernels",
        "//tensorflow/contrib/tensor_forest:model_ops_kernels",
        "//tensorflow/contrib/tensor_forest:stats_ops_kernels",
        "//tensorflow/contrib/tensor_forest:tensor_forest_kernels",
        "//tensorflow/contrib/text:all_kernels",
    ] + if_mpi(["//tensorflow/contrib/mpi_collectives:mpi_collectives_py"]) + if_cuda([
        "//tensorflow/contrib/nccl:nccl_kernels",
    ]) + select({
        "//tensorflow:with_kafka_support_windows_override": [],
        "//tensorflow:with_kafka_support": [
            "//tensorflow/contrib/kafka:dataset_kernels",
        ],
        "//conditions:default": [],
    }) + select({
        "//tensorflow:with_aws_support_windows_override": [],
        "//tensorflow:with_aws_support": [
            "//tensorflow/contrib/kinesis:dataset_kernels",
        ],
        "//conditions:default": [],
    }),
)

cc_library(
    name = "contrib_ops_op_lib",
    visibility = ["//visibility:public"],
    deps = [
        "//tensorflow/contrib/boosted_trees:boosted_trees_ops_op_lib",
        "//tensorflow/contrib/coder:all_ops",
        "//tensorflow/contrib/data:dataset_ops_op_lib",
        "//tensorflow/contrib/factorization:all_ops",
        "//tensorflow/contrib/framework:all_ops",
        "//tensorflow/contrib/input_pipeline:input_pipeline_ops_op_lib",
        "//tensorflow/contrib/layers:sparse_feature_cross_op_op_lib",
        "//tensorflow/contrib/nccl:nccl_ops_op_lib",
        "//tensorflow/contrib/nearest_neighbor:nearest_neighbor_ops_op_lib",
        "//tensorflow/contrib/rnn:all_ops",
        "//tensorflow/contrib/seq2seq:beam_search_ops_op_lib",
        "//tensorflow/contrib/tensor_forest:model_ops_op_lib",
        "//tensorflow/contrib/tensor_forest:stats_ops_op_lib",
        "//tensorflow/contrib/tensor_forest:tensor_forest_ops_op_lib",
        "//tensorflow/contrib/text:all_ops",
        "//tensorflow/contrib/tpu:all_ops",
    ] + select({
        "//tensorflow:with_kafka_support_windows_override": [],
        "//tensorflow:with_kafka_support": [
            "//tensorflow/contrib/kafka:dataset_ops_op_lib",
        ],
        "//conditions:default": [],
    }) + select({
        "//tensorflow:with_aws_support_windows_override": [],
        "//tensorflow:with_aws_support": [
            "//tensorflow/contrib/kinesis:dataset_ops_op_lib",
        ],
        "//conditions:default": [],
    }),
)
