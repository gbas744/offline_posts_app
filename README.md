 # Dominance Posts App (Flutter + Hive)
## 📌 Overview
This is a robust, offline-first Flutter application developed as part of the Section 5 Assignment. It demonstrates the power of separating the UI layer from the data layer and utilizing local NoSQL databases to create an unbreakable user experience.

The app fetches posts from the JSONPlaceholder API, caches them locally using Hive, and allows users to seamlessly save their favorite posts. Even when the internet is entirely cut off, the system survives and serves the cached data flawlessly.

## ✨ Core Features
Offline Survival: Gracefully falls back to local data (Hive) when network requests fail, ensuring zero downtime.

Hive Integration: Utilizes a lightweight, blazing-fast local NoSQL database to store complex Dart objects (HiveObject).

Favorites System: A dedicated, isolated Hive box (favoritesBox) to manage user preferences persistently across app restarts.

Reactive UI: Built with ValueListenableBuilder to reactively update the UI the moment the underlying Hive box changes, without unnecessary rebuilds.

State Handling: Handles three states seamlessly: Loading, Error (No internet + No cache), and Data.

## 📂 Project Structure
The app is split into small layers to keep the code organized:

<img width="872" height="342" alt="image" src="https://github.com/user-attachments/assets/c8616150-68eb-4bdc-8e90-868416e2962d" />

    
## 🚀 How to Run
bash
flutter pub get
dart run build_runner build --delete-conflicting-outputs
flutter run

## 📸 Proof of Concept (Screenshots)
1. The Main Dashboard (Posts loaded from API)
The initial state displaying all available posts.
<img width="1362" height="681" alt="posts_online" src="https://github.com/user-attachments/assets/6d4ae95c-938e-403a-89d9-fd2b027f881d" />


2. Active Selection (Favoriting Posts)
Tapping the star toggles the favorite and updates the icon immediately with a solid star.
<img width="1362" height="652" alt="favorite_toggle" src="https://github.com/user-attachments/assets/32fb8f0f-8441-46a7-83bd-67218c54530b" />

3. The Inner Circle (Favorites Screen)
A dedicated space displaying only the posts the user has chosen to keep.
<img width="1359" height="336" alt="favorites_screen" src="https://github.com/user-attachments/assets/14ce0c46-0118-4277-ba54-0fd32e635f9e" />

4. Empty Favorites
Friendly message displayed when the box is empty.
<img width="1361" height="620" alt="favorites_empty" src="https://github.com/user-attachments/assets/29357b7a-ccb1-4ed9-bbed-514ec2a96b03" />

5. Absolute Dominance (Offline Mode)
The system running independently in Airplane Mode (API blocked via DevTools), successfully bypassing connection errors and relying solely on the Hive cache.
<img width="1363" height="683" alt="posts_offline" src="https://github.com/user-attachments/assets/c9a1259d-8810-455b-ac18-b8ea68f28d86" />
(Console proving data loaded from Hive offline)
<img width="1024" height="264" alt="console_offline" src="https://github.com/user-attachments/assets/f8ec29d2-9714-45d1-8c26-e351b1b3b978" />

6. Favorites Survive Offline
Favorites are still there even when the internet is entirely cut off.
<img width="1365" height="667" alt="favorites_offline" src="https://github.com/user-attachments/assets/8a3f1386-e626-4b4f-9c58-170bb28f647a" />

7. Edge Case: No Internet & No Cached Data
The error screen shown when there is no connection and the Hive cache is empty.
<img width="1365" height="631" alt="error" src="https://github.com/user-attachments/assets/e307d972-6a61-45ec-8acc-26b160f31807" />

## 🧠 Design Notes
Isolated Favorites: Favorites live in their own box because getPosts() calls postsBox.clear() on every successful refresh.

Copy vs Reference: A copy of the post is saved in favoritesBox, because a HiveObject can belong to only one box at a time.

Fast Lookups: The post id is used as the key, so containsKey / delete are O(1) and extremely fast.

Reactive Stars: ValueListenableBuilder rebuilds the stars instantly when the box changes.

## 🛠️ Tech Stack
Framework: Flutter / Dart

Networking: http package

Local Storage: hive & hive_flutter

Code Generation: build_runner & hive_generator
