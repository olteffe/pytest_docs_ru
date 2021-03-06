.. _existingtestsuite:

Использование ``pytest`` с существующими наборами тестов
===========================================================


``pytest`` можно использовать с большинством существующих наборов тестов,
однако его поведение отличается от поведения других фреймворков, таких как
:ref:`nose <noseintegration>` или встроенный в ``Python`` ``unittest``.

Запуск существующих наборов тестов с помощью ``pytest``
--------------------------------------------------------

Допустим, вы хотите присоединиться к какому-либо существующему репозитарию.
После того, как вы  спомощью какой-то системы контроля версий
получите локальную копию кода и установите виртуальное окружение,
возможно, вам захочется запустить в корне проекта:

.. code-block:: bash

    cd <repository>
    pip install -e .  # альтернативная виртуальная среда, включающая
                      # 'python setup.py develop' и 'conda develop'

Это даст возможность создать символическую ссылку на ваш код, которая позволит его редактировать,
в то время как ваши тесты будут запускаться на нем, как на установленном пакете.

Установка вашего проекта в режиме разработки позволит вам избежать
переустановки пакета каждый раз, когда вы хотите запустить тесты.
Это удобнее, чем возиться с ``sys.path``, чтобы указать путь к вашим тестам
в локальном коде.

Советуем также рассмотреть возможность использования :ref:`tox <use tox>`.

.. include:: links.inc
