программа для умножения точки кривой на скаляр.
задаётся только скаляр.

остальные параметры кривой следующие:
p = FFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF43
a = FFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF40
b = 77CE6C1515F3A8EDD2C13AABE4D8FBBE4CF55069978B9253B22E7D6BD69C03F1
gx = 0
gy = 6BF7FC3CFB16D69F5CE4C9A351D6835D78913966C408F6521E29CF1804516A93

Вычисление точки происходит по методу double-and-add

В стандарте все числа в шестандцатеричной системе даны в формате LITTLE Endian,
 а программа работает с числами в формате BIG Endian,
 поэтому при ручном копировании из стандарта необходимо
 их конвертировать с помощью конвертера
ссылка на конвертер
http://www.save-editor.com/tools/wse_hex.html#littleendian

примерное время выполнения - 15-30 секунд
во время выполнения программа не реагирует ни на какие действия
для открытия в браузере без сервера использовать microsoft edge,
 иначе в папке compiled_project выполнить команду:
 node server.js
страницца будет доступна по адресу  http://127.0.0.1:3000/

как скомпилировать:

--установить EMSDK [ссылка с инструкциями по установке](https://emscripten.org/docs/getting_started/downloads.html)

--перейти в папку проекта!

--активировать emsdk
emsdk activate latest

--для создания папки проекта
mkdir compiled_project

--для компиляции проекта в webasm, экспортируется только функция mult, 'ccal','cwrap' нужны для вызова функции
emcc EC/Project1/Source.cpp EC/Project1/NumeralConverter.cpp EC/BigInteger.cpp EC/EllipticCurve.cpp EC/point.cpp -O3 -s WASM=1 -s EXPORTED_FUNCTIONS="['_mult']" -s EXPORTED_RUNTIME_METHODS="['ccall','cwrap']" -o compiled_project/EC.html --shell-file assets/shell_minimal.html -s ERROR_ON_UNDEFINED_SYMBOLS=0 -s ASSERTIONS=1

--для перенесения файлов с кастомными скриптами в папку проекта 
cp assets/custom_script.js compiled_project
cp assets/server.js compiled_project