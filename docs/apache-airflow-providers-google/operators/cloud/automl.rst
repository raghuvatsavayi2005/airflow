 .. Licensed to the Apache Software Foundation (ASF) under one
    or more contributor license agreements.  See the NOTICE file
    distributed with this work for additional information
    regarding copyright ownership.  The ASF licenses this file
    to you under the Apache License, Version 2.0 (the
    "License"); you may not use this file except in compliance
    with the License.  You may obtain a copy of the License at

 ..   http://www.apache.org/licenses/LICENSE-2.0

 .. Unless required by applicable law or agreed to in writing,
    software distributed under the License is distributed on an
    "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
    KIND, either express or implied.  See the License for the
    specific language governing permissions and limitations
    under the License.

Google Cloud AutoML Operators
=======================================

The `Google Cloud AutoML <https://cloud.google.com/automl/docs/>`__
makes the power of machine learning available to you even if you have limited knowledge
of machine learning. You can use AutoML to build on Google's machine learning capabilities
to create your own custom machine learning models that are tailored to your business needs,
and then integrate those models into your applications and web sites.

Prerequisite Tasks
^^^^^^^^^^^^^^^^^^

.. include:: /operators/_partials/prerequisite_tasks.rst

.. _howto/operator:CloudAutoMLDocuments:
.. _howto/operator:AutoMLCreateDatasetOperator:
.. _howto/operator:AutoMLImportDataOperator:
.. _howto/operator:AutoMLTablesUpdateDatasetOperator:

Creating Datasets
^^^^^^^^^^^^^^^^^

To create a Google AutoML dataset you can use
:class:`~airflow.providers.google.cloud.operators.automl.AutoMLCreateDatasetOperator`.
The operator returns dataset id in :ref:`XCom <concepts:xcom>` under ``dataset_id`` key.

.. exampleinclude:: /../../tests/system/providers/google/cloud/automl/example_automl_dataset.py
    :language: python
    :dedent: 4
    :start-after: [START howto_operator_automl_create_dataset]
    :end-before: [END howto_operator_automl_create_dataset]

After creating a dataset you can use it to import some data using
:class:`~airflow.providers.google.cloud.operators.automl.AutoMLImportDataOperator`.

.. exampleinclude:: /../../tests/system/providers/google/cloud/automl/example_automl_dataset.py
    :language: python
    :dedent: 4
    :start-after: [START howto_operator_automl_import_data]
    :end-before: [END howto_operator_automl_import_data]

To update dataset you can use
:class:`~airflow.providers.google.cloud.operators.automl.AutoMLTablesUpdateDatasetOperator`.

.. exampleinclude:: /../../tests/system/providers/google/cloud/automl/example_automl_dataset.py
    :language: python
    :dedent: 4
    :start-after: [START howto_operator_automl_update_dataset]
    :end-before: [END howto_operator_automl_update_dataset]

.. _howto/operator:AutoMLTablesListTableSpecsOperator:
.. _howto/operator:AutoMLTablesListColumnSpecsOperator:

Listing Table And Columns Specs
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

To list table specs you can use
:class:`~airflow.providers.google.cloud.operators.automl.AutoMLTablesListTableSpecsOperator`.

.. exampleinclude:: /../../tests/system/providers/google/cloud/automl/example_automl_dataset.py
    :language: python
    :dedent: 4
    :start-after: [START howto_operator_automl_specs]
    :end-before: [END howto_operator_automl_specs]

To list column specs you can use
:class:`~airflow.providers.google.cloud.operators.automl.AutoMLTablesListColumnSpecsOperator`.

.. exampleinclude:: /../../tests/system/providers/google/cloud/automl/example_automl_dataset.py
    :language: python
    :dedent: 4
    :start-after: [START howto_operator_automl_column_specs]
    :end-before: [END howto_operator_automl_column_specs]

.. _howto/operator:AutoMLTrainModelOperator:
.. _howto/operator:AutoMLGetModelOperator:
.. _howto/operator:AutoMLDeployModelOperator:
.. _howto/operator:AutoMLDeleteModelOperator:

Operations On Models
^^^^^^^^^^^^^^^^^^^^

To create a Google AutoML model you can use
:class:`~airflow.providers.google.cloud.operators.automl.AutoMLTrainModelOperator`.
The operator will wait for the operation to complete. Additionally the operator
returns the id of model in :ref:`XCom <concepts:xcom>` under ``model_id`` key.

This Operator is deprecated when running for text, video and vision prediction and will be removed soon.
All the functionality of legacy AutoML Natural Language, Vision, Video Intelligence and new features are
available on the Vertex AI platform. Please use
:class:`~airflow.providers.google.cloud.operators.vertex_ai.auto_ml.CreateAutoMLTextTrainingJobOperator`,
:class:`~airflow.providers.google.cloud.operators.vertex_ai.auto_ml.CreateAutoMLImageTrainingJobOperator` or
:class:`~airflow.providers.google.cloud.operators.vertex_ai.auto_ml.CreateAutoMLVideoTrainingJobOperator`.

You can find example on how to use VertexAI operators for AutoML Natural Language classification here:

.. exampleinclude:: /../../tests/system/providers/google/cloud/automl/example_automl_nl_text_classification.py
    :language: python
    :dedent: 4
    :start-after: [START howto_cloud_create_text_classification_training_job_operator]
    :end-before: [END howto_cloud_create_text_classification_training_job_operator]

Additionally, you can find example on how to use VertexAI operators for AutoML Vision classification here:

.. exampleinclude:: /../../tests/system/providers/google/cloud/automl/example_automl_vision_classification.py
    :language: python
    :dedent: 4
    :start-after: [START howto_cloud_create_image_classification_training_job_operator]
    :end-before: [END howto_cloud_create_image_classification_training_job_operator]

Example on how to use VertexAI operators for AutoML Video Intelligence classification you can find here:

.. exampleinclude:: /../../tests/system/providers/google/cloud/automl/example_automl_video_classification.py
    :language: python
    :dedent: 4
    :start-after: [START howto_cloud_create_video_classification_training_job_operator]
    :end-before: [END howto_cloud_create_video_classification_training_job_operator]

When running Vertex AI Operator for training data, please ensure that your data is correctly stored in Vertex AI
datasets. To create and import data to the dataset please use
:class:`~airflow.providers.google.cloud.operators.vertex_ai.dataset.CreateDatasetOperator`
and
:class:`~airflow.providers.google.cloud.operators.vertex_ai.dataset.ImportDataOperator`

.. exampleinclude:: /../../tests/system/providers/google/cloud/automl/example_automl_model.py
    :language: python
    :dedent: 4
    :start-after: [START howto_operator_automl_create_model]
    :end-before: [END howto_operator_automl_create_model]

To get existing model one can use
:class:`~airflow.providers.google.cloud.operators.automl.AutoMLGetModelOperator`.

.. exampleinclude:: /../../tests/system/providers/google/cloud/automl/example_automl_model.py
    :language: python
    :dedent: 4
    :start-after: [START howto_operator_get_model]
    :end-before: [END howto_operator_get_model]

Once a model is created it could be deployed using
:class:`~airflow.providers.google.cloud.operators.automl.AutoMLDeployModelOperator`.

.. exampleinclude:: /../../tests/system/providers/google/cloud/automl/example_automl_model.py
    :language: python
    :dedent: 4
    :start-after: [START howto_operator_deploy_model]
    :end-before: [END howto_operator_deploy_model]

If you wish to delete a model you can use
:class:`~airflow.providers.google.cloud.operators.automl.AutoMLDeleteModelOperator`.

.. exampleinclude:: /../../tests/system/providers/google/cloud/automl/example_automl_model.py
    :language: python
    :dedent: 4
    :start-after: [START howto_operator_automl_delete_model]
    :end-before: [END howto_operator_automl_delete_model]

.. _howto/operator:AutoMLPredictOperator:
.. _howto/operator:AutoMLBatchPredictOperator:

Making Predictions
^^^^^^^^^^^^^^^^^^

To obtain predictions from Google Cloud AutoML model you can use
:class:`~airflow.providers.google.cloud.operators.automl.AutoMLPredictOperator` or
:class:`~airflow.providers.google.cloud.operators.automl.AutoMLBatchPredictOperator`. In the first case
the model must be deployed.

.. exampleinclude:: /../../tests/system/providers/google/cloud/automl/example_automl_model.py
    :language: python
    :dedent: 4
    :start-after: [START howto_operator_prediction]
    :end-before: [END howto_operator_prediction]

.. exampleinclude:: /../../tests/system/providers/google/cloud/automl/example_automl_model.py
    :language: python
    :dedent: 4
    :start-after: [START howto_operator_batch_prediction]
    :end-before: [END howto_operator_batch_prediction]

.. _howto/operator:AutoMLListDatasetOperator:
.. _howto/operator:AutoMLDeleteDatasetOperator:

Listing And Deleting Datasets
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

You can get a list of AutoML datasets using
:class:`~airflow.providers.google.cloud.operators.automl.AutoMLListDatasetOperator`. The operator returns list
of datasets ids in :ref:`XCom <concepts:xcom>` under ``dataset_id_list`` key.

.. exampleinclude:: /../../tests/system/providers/google/cloud/automl/example_automl_dataset.py
    :language: python
    :dedent: 4
    :start-after: [START howto_operator_list_dataset]
    :end-before: [END howto_operator_list_dataset]

To delete a dataset you can use :class:`~airflow.providers.google.cloud.operators.automl.AutoMLDeleteDatasetOperator`.
The delete operator allows also to pass list or coma separated string of datasets ids to be deleted.

.. exampleinclude:: /../../tests/system/providers/google/cloud/automl/example_automl_dataset.py
    :language: python
    :dedent: 4
    :start-after: [START howto_operator_delete_dataset]
    :end-before: [END howto_operator_delete_dataset]

Reference
^^^^^^^^^

For further information, look at:

* `Client Library Documentation <https://googleapis.github.io/google-cloud-python/latest/automl/index.html>`__
* `Product Documentation <https://cloud.google.com/automl/docs/>`__
