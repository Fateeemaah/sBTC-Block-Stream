## sBTC-Block-Stream - Decentralized Video Streaming Platform 

### Overview

This project represents a decentralized video streaming platform built using smart contracts on the Stacks blockchain. The platform allows content creators to upload, manage, and monetize their videos. Users can purchase or subscribe to premium content, while administrators manage platform settings and policies. The system also tracks video views and revenue, distributing funds to the appropriate stakeholders.

### Key Features

1. **Content Creation & Uploading:**
   - Content creators can register, upload videos, and set a price for access.
   - Each video is uniquely identified by a video ID and includes metadata such as title, description, content hash, price, creation date, views, and revenue.

2. **User Interaction:**
   - Users can purchase videos using STX tokens.
   - Users can subscribe to a premium service with a subscription duration and receive access to exclusive content.

3. **Revenue Distribution:**
   - Each video has an associated revenue stream, with creators earning from video purchases.
   - Platform fee is applied to video revenue before distribution to creators.

4. **Access Control & Administration:**
   - The platform is managed by administrators who can set the platform fee, add new administrators, and pause the contract.
   - Only authorized content creators and administrators can perform certain actions.

5. **Governance:**
   - Governance proposals can be created, voted on, and executed by administrators, enabling decentralized decision-making for the platform's future.

6. **Premium Subscription:**
   - Users can subscribe to a premium service for access to exclusive content.
   - Subscriptions are tracked with expiry dates, ensuring only active subscribers can access premium content.

### Smart Contract Structure

The contract includes various sections such as constants, data storage, functions, and governance mechanisms.

#### Constants & Error Codes

- `contract-owner`: The principal address of the platform owner (administrator).
- Error codes such as `ERR-NOT-AUTHORIZED`, `ERR-ALREADY-EXISTS`, `ERR-INVALID-PARAMS`, etc., help manage different failure scenarios.

#### Data Storage

1. **Platform State:**
   - `contract-paused`: Indicates whether the contract is paused.
   - `platform-fee`: The percentage fee taken from the platform's revenue.
   - `next-video-id`: The next video ID to be assigned when a new video is uploaded.

2. **Access Control:**
   - `administrators`: A map that tracks administrators.
   - `content-creators`: A map that tracks content creators.
   - `premium-subscribers`: A map that tracks premium subscribers with subscription expiry dates.

3. **Content Storage:**
   - `videos`: A map that stores video metadata, including the creator, title, description, price, and views.

4. **Revenue Tracking:**
   - `creator-revenue`: A map that tracks the revenue of content creators.
   - `platform-revenue`: A map to track platform-wide revenue.

#### Functions

1. **Admin Functions:**
   - `set-platform-fee`: Allows administrators to update the platform fee.
   - `toggle-contract-pause`: Pauses or unpauses the contract.
   - `add-administrator`: Adds a new administrator.

2. **Creator Functions:**
   - `register-as-creator`: Allows a user to register as a content creator.
   - `upload-video`: Allows a content creator to upload a video with metadata such as title, description, content hash, and price.

3. **User Functions:**
   - `purchase-video`: Allows users to purchase a video.
   - `subscribe-premium`: Allows users to subscribe to premium content for a specified duration.

4. **Getter Functions:**
   - `get-video-details`: Retrieves the details of a video.
   - `get-creator-revenue`: Retrieves the revenue earned by a creator.
   - `is-premium-subscriber`: Checks if a user is a premium subscriber.

#### Authorization

The smart contract uses authorization checks to ensure that only authorized users can perform certain actions:

- `is-admin`: Checks if the sender is an administrator.
- `is-creator`: Checks if the sender is a content creator.
- `is-contract-owner`: Checks if the sender is the contract owner.
- `check-admin`: Ensures the sender is an administrator.

#### Governance

Governance proposals allow administrators to propose and vote on changes to the platform. Proposals include a title, description, proposer, vote counts, and an execution status.

### Contract Initialization

Upon contract deployment, the contract owner is initialized as the first administrator. The platform's revenue map is also initialized with a total revenue of 0.

### Usage

1. **Uploading Videos**: Content creators must first register as a creator using `register-as-creator`. After that, they can upload videos using the `upload-video` function.

2. **Purchasing Videos**: Users can purchase videos by calling the `purchase-video` function and paying the specified price in STX tokens.

3. **Subscription to Premium Content**: Users can subscribe to premium content by sending the required amount of STX to the contract owner via the `subscribe-premium` function.

4. **Admin Actions**: Administrators can modify the platform fee, pause the contract, and add new administrators.

### Security Considerations

1. **Pausing the Contract**: The contract can be paused at any time by an administrator, which disables user interactions until it is resumed.

2. **Error Handling**: Various assertions are used throughout the contract to ensure only valid actions are taken (e.g., ensuring that only valid video IDs or non-empty strings are processed).

3. **Revenue Split**: Platform revenue is managed transparently, with a platform fee deducted from creator earnings.

---
