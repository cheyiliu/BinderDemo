This is a bare bones example of how to use Android IPC binders from native C++
code. For some high-level explanations see the following two blog posts:

- http://ebixio.com/blog/2012/07/07/using-android-ipc-binders-from-native-code/
- http://ebixio.com/blog/2011/01/03/the-android-ipc-system/

```
 * To view the log output:
 *      adb logcat -v time binder_demo:* *:S
 *
 * To run, create 2 adb shell sessions. In the first one run "binder" with no
 * arguments to start the service. In the second one run "binder N" where N is
 * an integer, to start a client that connects to the service and calls push(N),
 * alert(), and add(N, 5).
```

I compiled in 4.2 source code and the output log is,
```
09-30 15:41:40.256 D/binder_demo( 8003): We're the service
09-30 15:41:40.256 D/binder_demo( 8003): IDemo::IDemo()
09-30 15:41:40.256 D/binder_demo( 8003): Demo service is now ready


09-30 15:42:03.726 D/binder_demo( 8014): We're the client: 100
09-30 15:42:03.726 D/binder_demo( 8014): IDemo::IDemo()
09-30 15:42:03.726 D/binder_demo( 8014): BpDemo::BpDemo()
09-30 15:42:03.726 D/binder_demo( 8014): BpDemo::alert()
09-30 15:42:03.726 D/binder_demo( 8003): BnDemo::onTransact(1) 17
09-30 15:42:03.726 D/binder_demo( 8003): Demo::alert()
09-30 15:42:03.726 D/binder_demo( 8003): BnDemo::onTransact(2) 16
09-30 15:42:03.736 D/binder_demo( 8003): BnDemo::onTransact got 100
09-30 15:42:03.736 D/binder_demo( 8003): Demo::push(100)
09-30 15:42:03.736 D/binder_demo( 8014): BpDemo::push(100)
09-30 15:42:03.736 D/binder_demo( 8003): BnDemo::onTransact(3) 16
09-30 15:42:03.736 D/binder_demo( 8003): Demo::add(100, 5)
09-30 15:42:03.736 D/binder_demo( 8003): BnDemo::onTransact add(100, 5) = 105
09-30 15:42:03.736 D/binder_demo( 8014): BpDemo::add transact reply
09-30 15:42:03.736 D/binder_demo( 8014): BpDemo::add(100, 5) = 105 (status: 0)
09-30 15:42:03.736 D/binder_demo( 8014): Addition result: 100 + 5 = 105
09-30 15:42:03.736 D/binder_demo( 8014): IDemo::~IDemo()

```
