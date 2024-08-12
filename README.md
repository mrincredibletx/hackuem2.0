# `sender::user_info` Module

The `sender::user_info` module provides functionality for managing user profiles in a blockchain-based application. This module allows you to set and retrieve a user's username. 

## Overview

### Data Structures

- **UserProfile**: A struct that represents a user profile. It contains a single field:
  - `username`: A `String` that stores the username of the user.

### Functions

1. **`get_username(user_addr: address): String`**

   Retrieves the username of a user given their address.

   - **Parameters**:
     - `user_addr`: The address of the user whose username is to be fetched.
   
   - **Returns**: The username of the user as a `String`.

   - **Acquires**: `UserProfile` resource at the provided address.

2. **`set_username(user_account: &signer, username_raw: vector<u8>)`**

   Sets or updates the username for the given user account.

   - **Parameters**:
     - `user_account`: A signer reference to the user's account that will be updated.
     - `username_raw`: A vector of bytes (`vector<u8>`) representing the raw username input in UTF-8 encoding.

   - **Acquires**: `UserProfile` resource for the caller’s address.

   - **Behavior**:
     - If no `UserProfile` exists for the user address, a new `UserProfile` resource is created and initialized with the provided username.
     - If a `UserProfile` already exists, it updates the username field with the new value.

## Example Usage

### Setting a Username

To set or update a username for a user:

```move
import sender::user_info;

public fun set_user_username(account: &signer, new_username: vector<u8>) {
    user_info::set_username(account, new_username);
}
