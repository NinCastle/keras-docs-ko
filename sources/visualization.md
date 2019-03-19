
## 모델 시각화 

Keras는 keras 모델을 그리기 위한 유용한 함수를 제공한다(`graphviz`를 사용).


아래는 코드는 그래프 그림과 모델을 세이브 하는 코드이다:
```python
from keras.utils import plot_model
plot_model(model, to_file='model.png')
```

`plot_model`는 네 가지 인자 옵션을 가지가고 있다:

- `show_shapes` (defaults to False) controls whether output shapes are shown in the graph.
- `show_layer_names` (defaults to True) controls whether layer names are shown in the graph.
- `expand_nested` (defaults to False) controls whether to expand nested models into clusters in the graph.
- `dpi` (defaults to 96) controls image dpi.

또한 `pydot.Graph` object를 가져와 직접 render 할 수 있다.  
예를 들어 ipython notebook에서 보여준다면 :
```python
from IPython.display import SVG
from keras.utils import model_to_dot

SVG(model_to_dot(model).create(prog='dot', format='svg'))
```

## 학습 기록 시각화

Keras `Model`의 `fit()` 메소드는 `History` object를 리턴 한다. 
The `fit()` method on a Keras `Model` returns a `History` object. The `History.history` attribute is a dictionary recording training loss values and metrics values at successive epochs, as well as validation loss values and validation metrics values (if applicable). Here is a simple example using `matplotlib` to generate loss & accuracy plots for training & validation:

```python
import matplotlib.pyplot as plt

history = model.fit(x, y, validation_split=0.25, epochs=50, batch_size=16, verbose=1)

# Plot training & validation accuracy values
plt.plot(history.history['acc'])
plt.plot(history.history['val_acc'])
plt.title('Model accuracy')
plt.ylabel('Accuracy')
plt.xlabel('Epoch')
plt.legend(['Train', 'Test'], loc='upper left')
plt.show()

# Plot training & validation loss values
plt.plot(history.history['loss'])
plt.plot(history.history['val_loss'])
plt.title('Model loss')
plt.ylabel('Loss')
plt.xlabel('Epoch')
plt.legend(['Train', 'Test'], loc='upper left')
plt.show()
```
