ThingsBoard API client library for Dart developers. Provides model objects and services to communicate with ThingsBoard platform using RESTful APIs and WebSocket protocol.
Current client version is compatible with ThingsBoard starting from version 3.4.2.

## Usage

A simple usage example:

```dart
import 'package:thingsboard_client/thingsboard_client.dart';

main() async {
    try {
      var tbClient = ThingsboardClient('https://demo.thingsboard.io');
      await tbClient.login(LoginRequest('tenant@thingsboard.org', 'tenant'));

      print('isAuthenticated=${tbClient.isAuthenticated()}');

      print('authUser: ${tbClient.getAuthUser()}');

      var currentUserDetails = await tbClient.getUserService().getUser();
      print('currentUserDetails: $currentUserDetails');

      await tbClient.logout();

    } catch (e, s) {
        print('Error: $e');
        print('Stack: $s');
    }
}
```

## Features and bugs

Please file feature requests and bugs at the [issue tracker][tracker].

[tracker]: https://github.com/thingsboard/dart_thingsboard_client/issues

## 修改日志
1. thingsboard_client-1.0.4\lib\src\service\device_service.dart  
   增加设备与user的对应函数，适配设备分配逻辑的变化  
   新增函数：
   - assignDeviceToUser 对应 assignDeviceToCustomer
   - unassignDeviceFromUser 对应 unassignDeviceFromCustomer
   - getUserDevices 对应 getCustomerDevices
   - getUserDeviceInfos 对应 getCustomerDeviceInfos
2. thingsboard_client-1.0.4\lib\src\model\device_models.dart  
   在device中增加userId字段等，适配设备分配逻辑变化后的设备信息  
   新增：customerId 对应位置增加 userId 共四处
3. 第2个修改后有bug，缺少文件，无法编译成功  
   添加has_user_id.dart文件。  
   在device_models.dart中导入has_user_id.dart和id/user_id.dart，在Device类名部分，HasCustomerId后增加HasUserId。  
   修改后，可编译成功。
