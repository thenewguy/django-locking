Django-locking
==============
Usage
-----
The simplest use is by using it as a context manager:

::

    with NonBlockingLock.objects.acquire_lock(obj=model_obj):
        model_obj.do_something()

Or you can keep track of the lock yourself:

::

    try:
        lock = NonBlockingLock.objects.acquire_lock(obj=model_obj)
    except AlreadyLocked:
        return False

    model_obj.do_something()
    lock.release()

If you have no Django model, or you want to be able to specify the lock name
yourself, you can do that too::

    # this will raise AlreadyLocked, if it's locked
    lock = NonBlockingLock.objects.acquire_lock(lock_name='my_lock')
    do_something()
    lock.release()

Test
-----
You can run the tests with
::

    python setup.py test

Wishlist
--------
- Add lock time-out (try to aquire a lock for up to a given TIME_OUT), like
  `lockfile's <http://packages.python.org/lockfile/>`_ `FileLock.aquire
  <http://packages.python.org/lockfile/lockfile.html#lockfile.FileLock.acquire>`_
- Global locks (for instance on a whole Model not just an object)

Releases
--------
v1.1.0:
  Rename model to NonBlockingLock and add additional features
v1.0.1:
  Corrected tests and code clean-up
v1.0.0:
  Intial release.
