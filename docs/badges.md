# Badges system

Badges are tokens which can represent various informations, such as access to a contest, belonging to a group, or completion of challenges, for instance.

They are attached to users, and some of them can even allow authentication of users from one platform to another.

## Badge verification

A badge can be an URL to a verification service, along with a code.

For instance, the [login-module](https://github.com/France-ioi/login-module) can be required to ask users who log in for a badge they acquired when participating in a contest on [bebras-platform](https://github.com/France-ioi/bebras-platform). The badge URL will then be `https://badges.example.com/path/to/badge`, where `path/to/badge` is the target badge we are requesting.

Users will be prompted for a code; they can either input a code, which will be checked against the badge verification service, or say they don't have the code. If they input a valid code, the login-module will then store the badge for this user. From then on, this badge will be presented to the login request origin upon each successful login. It can be used for instance in [AlgoreaPlatform](https://github.com/France-ioi/AlgoreaPlatform) to allow access to some content only to users with a certain badge.

The verification is done by a POST request to the badge URL. When the user inputs a code, the login-module will send a POST request to the badge URL, with the parameters `action='verifyCode'` and the user `code='abcdef'`. If the code is valid, bebras-platform will then answer with some information about the user who acquired the badge in JSON format:
```
{
    "sFirstName": "Example",
    "sLastName": "Name",
    "sSex": "Male",
    "sEmail": "name@example.com",
    "sZipcode": "12345",
    "franceioiID": "678"
}
```

The fields `sFirstName`, `sLastName`, `sSex`, `sEmail`, `sZipcode` are generic fields, but the answer can also contain fields specific to the badge, such as `franceioiID` in the example above.

If the code is invalid, the answer will be null.
