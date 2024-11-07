# UserInfoController Documentation

## Overview

`UserInfoController` is a Spring Boot controller class that handles user-related operations for Carlos Bakery. This includes user registration, login, password management, profile management, and exporting user-related data. The controller utilizes various HTTP methods (GET, POST, PUT) to perform these actions and interacts with the `UserHelper` class to execute the business logic.

## Class Diagram

```flowchart
classDiagram
    class UserInfoController {
        +UserHelper userHelper
        +createUser(SignupDomain, HttpServletResponse) UserInfoMessage
        +verifyOTP(SignupDomain, HttpServletRequest, HttpServletResponse) ResponseMessage<UserInfo>
        +facebookLogin(SignupDomain, HttpServletRequest, HttpServletResponse) UserInfoMessage
        +loginUser(String, String, String, String, int, HttpServletResponse) UserInfoMessage
        +forgetPassword(String, HttpServletResponse) ResponseStatus
        +resetpassword(String, String, String, String, HttpServletResponse) UserMessage
        +changePassword(String, String, String, HttpServletRequest, HttpServletResponse) UserMessage
        +getProfile(String, HttpServletResponse) ProfileWithCustomerResponse
        +updateUser(SignupDomain, HttpServletRequest, HttpServletResponse) UpdateUserMessage
        +editUser(SignupDomain, HttpServletRequest, HttpServletResponse) UpdateUserMessage
        +exportTransactionAndUserHistoryExcel(int, int, HttpServletRequest) ResponseMessage<ExportFiles>
        +logout(HttpServletRequest) ResponseStatus
        +updateDeviceToken(SignupDomain, HttpServletRequest) UserMessage
    }
    UserInfoController --> UserHelper
    UserInfoController --> SignupDomain
    UserInfoController --> HttpServletRequest
    UserInfoController --> HttpServletResponse
    UserInfoController --> UserInfo
    UserInfoController --> ExportFiles
    UserInfoController --> ResponseMessage
    UserInfoController --> ResponseStatus
    UserInfoController --> UpdateUserMessage
    UserInfoController --> UserInfoMessage
    UserInfoController --> UserMessage
    UserInfoController --> ProfileWithCustomerResponse
```

## Methods

### `createUser`

```java
@PostMapping("register")
public @ResponseBody UserInfoMessage createUser(@RequestBody SignupDomain signupObj, final HttpServletResponse response)
```

**Description:** Registers a new user.

**Parameters:**
- `signupObj` (SignupDomain): The signup information.
- `response` (HttpServletResponse): The HTTP response.

**Returns:** `UserInfoMessage` - The user information message after registration.

### `verifyOTP`

```java
@PostMapping("verificationlink")
public @ResponseBody ResponseMessage<UserInfo> verifyOTP(@RequestBody SignupDomain userObj, HttpServletRequest request, final HttpServletResponse response)
```

**Description:** Verifies the OTP sent to the user.

**Parameters:**
- `userObj` (SignupDomain): The user information.
- `request` (HttpServletRequest): The HTTP request.
- `response` (HttpServletResponse): The HTTP response.

**Returns:** `ResponseMessage<UserInfo>` - The response message after OTP verification.

### `facebookLogin`

```java
@PostMapping("sociallogin")
public @ResponseBody UserInfoMessage facebookLogin(@RequestBody SignupDomain userObj, HttpServletRequest request, final HttpServletResponse response)
```

**Description:** Logs in the user through Facebook.

**Parameters:**
- `userObj` (SignupDomain): The user information.
- `request` (HttpServletRequest): The HTTP request.
- `response` (HttpServletResponse): The HTTP response.

**Returns:** `UserInfoMessage` - The user information message after Facebook login.

### `loginUser`

```java
@PostMapping("login")
public @ResponseBody UserInfoMessage loginUser(@FormParam("email") String email, @FormParam("password") String password, @FormParam("deviceToken") String deviceToken, @FormParam("deviceType") String deviceType, @RequestParam(value="traffic", required=false, defaultValue="0") int traffic, final HttpServletResponse response)
```

**Description:** Logs in the user using email and password.

**Parameters:**
- `email` (String): The user's email.
- `password` (String): The user's password.
- `deviceToken` (String): The device token.
- `deviceType` (String): The device type.
- `traffic` (int): The traffic parameter.
- `response` (HttpServletResponse): The HTTP response.

**Returns:** `UserInfoMessage` - The user information message after login.

### `forgetPassword`

```java
@PostMapping("forgotpassword")
public @ResponseBody ResponseStatus forgetPassword(@RequestParam("email") String email, final HttpServletResponse response)
```

**Description:** Sends a password reset link to the user's email.

**Parameters:**
- `email` (String): The user's email.
- `response` (HttpServletResponse): The HTTP response.

**Returns:** `ResponseStatus` - The status of the password reset request.

### `resetpassword`

```java
@PostMapping("resetpassword")
public @ResponseBody UserMessage resetpassword(@RequestParam("email") String email, @RequestParam("newpassword") String newpassword, @RequestParam("confirmpassword") String confirmpassword, @FormParam("verificationCode") String verificationCode, final HttpServletResponse response)
```

**Description:** Resets the user's password.

**Parameters:**
- `email` (String): The user's email.
- `newpassword` (String): The new password.
- `confirmpassword` (String): The confirmation password.
- `verificationCode` (String): The verification code.
- `response` (HttpServletResponse): The HTTP response.

**Returns:** `UserMessage` - The user message after password reset.

### `changePassword`

```java
@PostMapping("changepassword")
public @ResponseBody UserMessage changePassword(@RequestParam("currentpassword") String currentpassword, @RequestParam("newpassword") String newpassword, @RequestParam("confirmpassword") String confirmpassword, final HttpServletRequest request, final HttpServletResponse response)
```

**Description:** Changes the user's password.

**Parameters:**
- `currentpassword` (String): The current password.
- `newpassword` (String): The new password.
- `confirmpassword` (String): The confirmation password.
- `request` (HttpServletRequest): The HTTP request.
- `response` (HttpServletResponse): The HTTP response.

**Returns:** `UserMessage` - The user message after password change.

### `getProfile`

```java
@GetMapping("getprofile")
public @ResponseBody ProfileWithCustomerResponse getProfile(@RequestParam(value="userid") String userid, final HttpServletResponse response)
```

**Description:** Retrieves the user's profile.

**Parameters:**
- `userid` (String): The user ID.
- `response` (HttpServletResponse): The HTTP response.

**Returns:** `ProfileWithCustomerResponse` - The user's profile information.

### `updateUser`

```java
@PostMapping("updateprofile")
public @ResponseBody UpdateUserMessage updateUser(@RequestBody SignupDomain obj, final HttpServletRequest request, final HttpServletResponse response)
```

**Description:** Updates the user's profile.

**Parameters:**
- `obj` (SignupDomain): The signup information.
- `request` (HttpServletRequest): The HTTP request.
- `response` (HttpServletResponse): The HTTP response.

**Returns:** `UpdateUserMessage` - The update user message.

### `editUser`

```java
@PutMapping("editprofile")
public @ResponseBody UpdateUserMessage editUser(@RequestBody SignupDomain obj, final HttpServletRequest request, final HttpServletResponse response)
```

**Description:** Edits the user's profile.

**Parameters:**
- `obj` (SignupDomain): The signup information.
- `request` (HttpServletRequest): The HTTP request.
- `response` (HttpServletResponse): The HTTP response.

**Returns:** `UpdateUserMessage` - The edit user message.

### `exportTransactionAndUserHistoryExcel`

```java
@GetMapping("/exportexcel")
public @ResponseBody ResponseMessage<ExportFiles> exportTransactionAndUserHistoryExcel(@RequestParam(value="type", required=false, defaultValue="0") int type, @RequestParam(value="offsetmin", required=false, defaultValue="0") int offsetmin, final HttpServletRequest request)
```

**Description:** Exports user transaction and history as an Excel file.

**Parameters:**
- `type` (int): The type of export.
- `offsetmin` (int): The offset in minutes.
- `request` (HttpServletRequest): The HTTP request.

**Returns:** `ResponseMessage<ExportFiles>` - The response message containing the exported files.

### `logout`

```java
@PutMapping("/revoke")
public @ResponseBody ResponseStatus logout(HttpServletRequest request)
```

**Description:** Logs out the user by revoking the session.

**Parameters:**
- `request` (HttpServletRequest): The HTTP request.

**Returns:** `ResponseStatus` - The status of the logout operation.

### `updateDeviceToken`

```java
@PostMapping("updatedevicetoken")
public @ResponseBody UserMessage updateDeviceToken(@RequestBody SignupDomain obj, final HttpServletRequest request)
```

**Description:** Updates the user's device token.

**Parameters:**
- `obj` (SignupDomain): The signup information.
- `request` (HttpServletRequest): The HTTP request.

**Returns:** `UserMessage` - The user message after updating the device token.
