
.. _`classic xunit`:
.. _xunitsetup:

Классический "setup" в стиле ``xunit``
=============================================

Этот раздел описывает популярный классический способ реализации
фикстур ("setup/teardown" методов) на уровнях модулей/классов/функций.

.. note::

    Поскольку эти методы просты и хорошо знакомы тем, кто уже использовал
    ``unittest`` or ``nose background``, вы также можете рассмотреть
    применение более мощного :ref:`механизма фикстур <fixture>`,
    который использует концепцию внедрения зависимостей, позволяя
    создавать более модальные и масштабируемые тесты, что особенно важно
    в больших проектах или при функциональном тестировании.
    В одном и том же файле можно использовать оба механизма,
    однако нужно иметь в виду, что подклассы ``unittest.TestCase``
    не способны принимать аргументы-фикстуры.


"setup/teardown" для модуля
----------------------------------------

Если у вас есть несколько тестовых функций и классов в отдельном модуле,
вы можете реализовать следующие методы-фикстуры, которые будут вызываться
только один раз для всех функций модуля:

.. code-block:: python

    def setup_module(module):
        """настройка любых состояний, специфичных для выполнения этого модуля """


    def teardown_module(module):
        """ очистка любых состояний, настроенных ранее с помощью метода
            setup_module
        """

Начиная с ``pytest-3.0``, параметр ``module`` можно не указывать

"setup/teardown" для класса
----------------------------------------

Аналогичные методы существуют и на уровне класса -
они будут вызваны до и после всех тестовых методов класса:

.. code-block:: python

    @classmethod
    def setup_class(cls):
        """ настройка любых состояний, специфичных для выполнения этого класса (который
        обычно содержит тесты).
        """


    @classmethod
    def teardown_class(cls):
       """ очистка любых состояний, настроенных ранее с помощью метода
           setup_class.
       """


"setup/teardown" для функций и методов
--------------------------------------------------

Аналогично, следующими методами можно "обернуть" каждый
вызов метода класса:

.. code-block:: python

    def setup_method(self, method):
        """ настройка любого состояния, связанного с выполнением этого метода класса.
        setup_method вызывается для каждого метода класса.
        """


    def teardown_method(self, method):
        """ очистка любого состояния, настроенного ранее с помощью вызова setup_method
        """

Начиная с ``pytest-3.0``, параметр ``method`` указывать не обязательно.

Если же вы предпрочитаете определять тестовые функции на уровне модуля
(без разнесения по классам), для них тоже можно реализовать фикстуры:

.. code-block:: python

    def setup_function(function):
        """ настройка любого состояния, связанного с выполнением данной функции.
        Вызывается для каждой тестовой функции модуля.
        """


    def teardown_function(function):
        """ очистка любого состояния, настроенного ранее с помощью вызова setup_function
        """

Начиная с ``pytest-3.0``, параметр ``function`` указывать не обязательно.

Замечания:

* Пары "setup/teardown" во время тестирования могут вызываться многократно.

* Функция "teardown" не будет вызвана, если соответствующая "setup" функция
  существует, но была пропущена или выдала ошибку.

* Вплоть до ``pytest-4.2``, для функций в стиле ``xunit`` не соблюдались правила
  задания области действия фикстур, поэтому, к примеру, могло случаться так,
  что ``setup_method`` вызывался до ``autouse`` фикстуры уровня сессии.

  Сейчас функции ``xunit`` интегрированы с механизмом фикстур, и для них
  применяются те же правила области действия, что и для вызова фикстур.

.. _`unittest.py module`: http://docs.python.org/library/unittest.html
