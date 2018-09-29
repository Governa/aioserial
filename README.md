# aioserial

A Python package that combines [asyncio](https://docs.python.org/3/library/asyncio.html) and [pySerial](https://github.com/pyserial/pyserial).

## API

### aioserial vs. pySerial

```py
>>> import aioserial
>>> import serial

>>> aioserial.Serial is serial.Serial
True
```


### AioSerial

```py
>>> import aioserial
>>> import serial

>>> isinstance(aioserial.AioSerial(), serial.Serial)
True

>>> issubclass(aioserial.AioSerial, serial.Serial)
True
```

#### Constructor

```py
aioserial_instance: aioserial.AioSerial = aioserial.AioSerial(
    # ... same with what can be passed to serial.Serial ...,
    loop: Optional[asyncio.AbstractEventLoop] = None)
```

#### Methods


##### read_async

```py
bytes_read: bytes = \
    await aioserial_instance.read_async(size: int = 1)
```

##### read_until_async

```py
at_most_certain_size_of_bytes_read: bytes = \
    await aioserial_instance.read_until_async(
        expected: bytes = serial.LF, size: Optional[int] = None)
```

##### readinto_async

```py
number_of_byte_read: int = \
    await aioserial_instance.readinto_async(b: Union[array.array, bytearray])
```

##### readline_async

```py
a_line_of_at_most_certain_size_of_bytes_read: bytes = \
    await aioserial_instance.readline_async(size: int = -1)
```

##### readlines_async

```py
lines_of_at_most_certain_size_of_bytes_read: bytes = \
    await aioserial_instance.readlines_async(hint: int = -1)
```

##### write_async

```py
number_of_byte_like_data_written: int = \
    await aioserial_instance.write_async(bytes_like_data)
```

##### writelines_async

```py
number_of_byte_like_data_in_the_given_list_written: int = \
    await aioserial_instance.writelines_async(list_of_bytes_like_data)
```

### Other APIs

All the other APIs in package [pySerial](https://github.com/pyserial/pyserial) are supported in [aioserial](https://github.com/changyuheng/aioserial) as [original](https://pyserial.readthedocs.io/).

## Why aioserial

* Want to use an asyncio-based but not (self-built) thread-based serial library.
* [pySerial-asyncio](https://github.com/pyserial/pyserial-asyncio) doesn't support Windows.
* APIs in all the packages ([pySerial-asyncio](https://github.com/pyserial/pyserial-asyncio), [asyncserial](https://github.com/xvzf/asyncserial-py)) that target the same goal are not designed in high level. You don't want to learn new APIs if you are already familiar with [pySerial](https://github.com/pyserial/pyserial).