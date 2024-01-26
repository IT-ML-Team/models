![Logo](https://storage.googleapis.com/tf_model_garden/tf_model_garden_logo.png)

# Welcome to the Model Garden for TensorFlow

The TensorFlow Model Garden is a repository with a number of different
implementations of state-of-the-art (SOTA) models and modeling solutions for
TensorFlow users. We aim to demonstrate the best practices for modeling so that
TensorFlow users can take full advantage of TensorFlow for their research and
product development.

To improve the transparency and reproducibility of our models, training logs on
[TensorBoard.dev](https://tensorboard.dev) are also provided for models to the
extent possible though not all models are suitable.

| Directory | Description |
|-----------|-------------|
| [official](official) | • A collection of example implementations for SOTA models using the latest TensorFlow 2's high-level APIs<br />• Officially maintained, supported, and kept up to date with the latest TensorFlow 2 APIs by TensorFlow<br />• Reasonably optimized for fast performance while still being easy to read |
| [research](research) | • A collection of research model implementations in TensorFlow 1 or 2 by researchers<br />• Maintained and supported by researchers |
| [community](community) | • A curated list of the GitHub repositories with machine learning models and implementations powered by TensorFlow 2 |
| [orbit](orbit) | • A flexible and lightweight library that users can easily use or fork when writing customized training loop code in TensorFlow 2.x. It seamlessly integrates with `tf.distribute` and supports running on different device types (CPU, GPU, and TPU). |

## [Announcements](https://github.com/tensorflow/models/wiki/Announcements)

## Contributions

[![help wanted:paper implementation](https://img.shields.io/github/issues/tensorflow/models/help%20wanted%3Apaper%20implementation)](https://github.com/tensorflow/models/labels/help%20wanted%3Apaper%20implementation)

If you want to contribute, please review the [contribution guidelines](https://github.com/tensorflow/models/wiki/How-to-contribute).

## License

[Apache License 2.0](LICENSE)


## Changes
```diff
Index: research/object_detection/packages/tf2/setup.py
IDEA additional info:
Subsystem: com.intellij.openapi.diff.impl.patch.CharsetEP
<+>UTF-8
===================================================================
diff --git a/research/object_detection/packages/tf2/setup.py b/research/object_detection/packages/tf2/setup.py
--- a/research/object_detection/packages/tf2/setup.py	(revision e39f2477ac207b2d0e15a8d9f172e07e76799eb0)
+++ b/research/object_detection/packages/tf2/setup.py	(date 1706260893367)
@@ -3,13 +3,10 @@
 from setuptools import find_packages
 from setuptools import setup
 
-# Note: adding apache-beam to required packages causes conflict with
-# tf-models-offical requirements. These packages request for incompatible
-# oauth2client package.
 REQUIRED_PACKAGES = [
     # Required for apache-beam with PY3
-    'avro-python3',
-    'apache-beam',
+    # 'avro-python3',
+    # 'apache-beam',
     'pillow',
     'lxml',
     'matplotlib',
@@ -21,24 +18,40 @@
     'lvis',
     'scipy',
     'pandas',
-    'tf-models-official'
+    'tf-models-official>=2.5.1',
+    'tensorflow_io',
+    'keras',
+    'pyparsing==2.4.7'  # TODO(b/204103388)
 ]
+
+pkg_dir_name = 'object_detection'
 
 setup(
-    name='object_detection',
-    version='0.1',
+    name='tf_models_research_object_detection',
+    version='2.8.0.post1',
     install_requires=REQUIRED_PACKAGES,
     include_package_data=True,
+    author='Google Inc.',
+    author_email='packages@tensorflow.org',
+    url='https://github.com/tensorflow/models',
+    license='Apache 2.0',
     packages=(
-        [p for p in find_packages() if p.startswith('object_detection')] +
-        find_packages(where=os.path.join('.', 'slim'))),
+            [p for p in find_packages() if p.startswith('object_detection')] +
+            [f'{pkg_dir_name}.{p}' for p in find_packages(where=os.path.join('.', 'slim'))]),
+
     package_dir={
-        'datasets': os.path.join('slim', 'datasets'),
-        'nets': os.path.join('slim', 'nets'),
-        'preprocessing': os.path.join('slim', 'preprocessing'),
-        'deployment': os.path.join('slim', 'deployment'),
-        'scripts': os.path.join('slim', 'scripts'),
+        f'{pkg_dir_name}.datasets': os.path.join('slim', 'datasets'),
+        f'{pkg_dir_name}.nets': os.path.join('slim', 'nets'),
+        f'{pkg_dir_name}.preprocessing': os.path.join('slim', 'preprocessing'),
+        f'{pkg_dir_name}.deployment': os.path.join('slim', 'deployment'),
+        f'{pkg_dir_name}.scripts': os.path.join('slim', 'scripts'),
     },
-    description='Tensorflow Object Detection Library',
+    description='Ready to use tensorflow research object_detection distribution for windows and linux.',
+    long_description='This is not an official package from the creators of tensorflow/models/research. '
+                     'The creator of these wheels does not hold any rights to tensorflow models as well as tensorflow. '
+                     'We do not give any support and are not liable for any damage caused by the use of this software. '
+                     '\n'
+                     'For more information about the copyright holders please visit '
+                     'https://github.com/tensorflow/models/tree/master/research/object_detection',
     python_requires='>3.6',
 )

```
