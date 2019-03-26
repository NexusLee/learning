### tf.contrib.tpu.TPUEstimatorSpec 优化器

### tf.estimator.EstimatorSpec 训练或者评估模型（运行在 cpu/gpu）
```py

  '''
  该类定义了一个具体的模型对象，但是参数之间互相有约束 
  mode: 定义了模型的类型，也就是上文ModeKeys类对象，依赖于不同的model对取值会有所要求： 
  如果mode==ModeKeys.TRAIN，此时模型类型为训练，则必须loss和train_op参数 
  如果mode==ModeKeys.EVAL，此时模型类型为评估，则必须loss参数 
  如果mode==ModeKeys.PREDICT`，此时模型类型为预测，则必须predictions 
  EstimatorSpec一般会配合Estimator类使用。
  '''
  def __new__(cls, 
    mode, 
    predictions=None, 
    loss=None, 
    train_op=None, 
    eval_metric_ops=None, 
    export_outputs=None, 
    training_chief_hooks=None, 
    training_hooks=None, 
    scaffold=None): 

  #调用Estimator
  tf.estimator.EstimatorSpec(
    model_fn, #模型函数
    model_dir=None, #存储目录
    config=None, #设置参数对象
    params=None, #超参数，将传递给model_fn使用
    warm_start_from=None #热启动目录路径
  )

```

### estimator.train(input_fn=train_input_fn, max_steps=num_train_steps)  训练模型
