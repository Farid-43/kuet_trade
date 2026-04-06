# KUET Trade - শুরুর জন্য প্রজেক্ট ব্যাখ্যা

এই ডকুমেন্টটি প্রজেক্টটা দ্রুত বোঝার জন্য একটি স্টার্টার গাইড।

এখনকার লক্ষ্য:

- পুরো অ্যাপের একটি ছোট, সহজ ভাষার ব্যাখ্যা দেওয়া
- পরে ফাইল-ভিত্তিক ফুল ডিটেইলস যোগ করার জন্য একটি রোডম্যাপ তৈরি করা

---

## 1) ছোট ব্যাখ্যা (First Look)

KUET Trade হলো KUET শিক্ষার্থীদের জন্য একটি iOS মার্কেটপ্লেস অ্যাপ।

মূল আইডিয়া:

- স্টুডেন্টরা অ্যাকাউন্ট খুলে লগইন করতে পারে
- তারা বই, ইলেকট্রনিকস ইত্যাদি আইটেম ছবি সহ পোস্ট করতে পারে
- অন্য স্টুডেন্টরা আইটেম ব্রাউজ, সার্চ, ফিল্টার করে সেলারকে কনট্যাক্ট করতে পারে
- সেলাররা নিজের বিজ্ঞাপন এডিট, sold মার্ক, অথবা ডিলিট করতে পারে

ব্যবহৃত টেকনোলজি:

- **SwiftUI**: UI তৈরির জন্য
- **MVVM-style structure**: Views + ViewModels + Services + Models
- **Firebase**:
  - Auth (login/signup)
  - Firestore (users + items data)
  - Storage (item images)

---

## 2) অ্যাপের হাই-লেভেল ফ্লো

1. অ্যাপ চালু হলে Firebase configure হয়
2. ContentView auth state চেক করে
3. auth চেক চললে launch animation দেখায়
4. user logged in থাকলে main tab app দেখায়
5. logged in না থাকলে login screen দেখায়
6. logged-in user যা করতে পারে:
   - আইটেম ব্রাউজ/সার্চ/ফিল্টার
   - আইটেম ডিটেইলস খুলে সেলারকে কনট্যাক্ট
   - নতুন ad পোস্ট
   - My Ads থেকে নিজের ad manage
   - profile দেখা এবং sign out

---

## 3) আর্কিটেকচার (সহজভাবে)

- **Models**: ডেটার গঠন (Item, KTUser)
- **Services**: Firebase এর সাথে যোগাযোগ (AuthService, FirestoreService, StorageService)
- **ViewModels**: business logic এবং screen state (AuthViewModel, ItemViewModel, PostItemViewModel)
- **Views**: UI screen/component
- **Utilities**: constants, extensions, network status, rule references

সহজভাবে ভাবলে:

- Views ডেটা দেখায়
- ViewModels ডেটা/স্টেট ম্যানেজ করে
- Services Firebase থেকে ডেটা আনে/সেভ করে
- Models ডেটার ফরম্যাট নির্ধারণ করে

---

## 4) ফাইল ম্যাপ (প্রতিটি ফাইলের দ্রুত কাজ)

### Root

- KUET_TradeApp.swift: অ্যাপের entry point, Firebase configure করে
- ContentView.swift: প্রথমে কোন screen দেখাবে তা ঠিক করে (launch/login/main tabs)
- GoogleService-Info.plist: Firebase project configuration

### Models

- Models/Item.swift: Item model + category/sort enums
- Models/User.swift: User model (KTUser)

### Services

- Services/AuthService.swift: signup/login/logout/reset password + auth listener
- Services/FirestoreService.swift: Firestore এ item CRUD
- Services/StorageService.swift: Firebase Storage এ image upload/delete

### ViewModels

- ViewModels/AuthViewModel.swift: auth state, form state, validation, user loading
- ViewModels/ItemViewModel.swift: item loading, search/filter/sort logic
- ViewModels/PostItemViewModel.swift: post/edit form logic, validation, image handling

### Utilities

- Utilities/Constants.swift: app constants (department, limit, path)
- Utilities/Extensions.swift: helper extensions (email/phone validation, trim, etc.)
- Utilities/NetworkMonitor.swift: internet monitor + offline banner
- Utilities/FirestoreRules.swift: Firebase security rules reference (ডকুমেন্টেশন, রান হয় না)

### Views (Main)

- Views/MainTabView.swift: main tab navigation (Home, Post, My Ads, Profile)

### Views/Auth

- Views/Auth/LoginView.swift: login screen
- Views/Auth/SignUpView.swift: sign-up screen
- Views/Auth/ForgotPasswordView.swift: password reset screen

### Views/Home

- Views/Home/HomeView.swift: browse/search/filter + item grid
- Views/Home/ItemCardView.swift: প্রতিটি item এর ছোট কার্ড
- Views/Home/ItemDetailView.swift: full item details + contact options

### Views/Post

- Views/Post/PostItemView.swift: নতুন listing তৈরি
- Views/Post/EditItemView.swift: existing listing edit

### Views/Profile

- Views/Profile/MyAdsView.swift: নিজের listing manage (active/sold/edit/delete)
- Views/Profile/ProfileView.swift: user profile, app share, sign out

### Views/Search

- Views/Search/SearchFilterView.swift: advanced search/filter sheet

### Views/Components

- Views/Components/ContactSellerButton.swift: call/WhatsApp/SMS actions
- Views/Components/ImagePicker.swift: camera/gallery picker bridge
- Views/Components/LaunchScreenView.swift: animated launch screen
- Views/Components/ShimmerView.swift: skeleton loading placeholders

---

## 5) এই প্রজেক্টে এখন যা কাজ করছে (Feature Snapshot)

- Authentication flow (signup/login/reset/logout)
- Firestore এ user profile data
- ছবি সহ item posting
- item browsing এবং detail page
- search + category + price + sort filters
- seller contact actions
- My Ads management (edit, sold toggle, delete)
- network state অনুযায়ী offline banner

---

## 6) শেখার সাজেস্টেড অর্ডার (Mac ছাড়াই)

নিচের ক্রমে কোড পড়লে পুরো প্রজেক্ট সহজে বোঝা যাবে:

1. KUET_TradeApp.swift
2. ContentView.swift
3. Views/MainTabView.swift
4. Models/\*
5. Services/\*
6. ViewModels/\*
7. Views/Auth/\*
8. Views/Home/\*
9. Views/Post/\*
10. Views/Profile/\*
11. Views/Search/\*
12. Views/Components/\*
13. Utilities/\*

---

## 7) পরের ধাপের প্ল্যান (আগামী সেশনগুলোতে)

আগামী স্টেপগুলোতে আমরা একে একে deep details যোগ করব:

- [ ] KUET_TradeApp.swift full explanation
- [ ] ContentView.swift full explanation
- [ ] AuthViewModel.swift full explanation
- [ ] AuthService.swift full explanation
- [ ] ItemViewModel.swift full explanation
- [ ] PostItemViewModel.swift full explanation
- [ ] FirestoreService.swift full explanation
- [ ] StorageService.swift full explanation
- [ ] সব view file full explanation (one by one)
- [ ] Utilities full explanation

যখন detailed mode শুরু করব, প্রতিটি ফাইল সেকশনে থাকবে:

- Purpose
- Key properties
- Key functions
- UI behavior (যদি view হয়)
- Data flow in/out
- ওই ফাইল থেকে আসতে পারে এমন common interview/defense প্রশ্ন

---

## 8) গুরুত্বপূর্ণ কথা

এই প্রজেক্টে beginner-friendly MVVM pattern এবং Firebase integration পরিষ্কারভাবে ও consistent ভাবে ব্যবহার করা হয়েছে। group academic project হিসেবে এটা ভালো ও practical base.

---

## 9) Function-by-Function Detailed Explanation (শুরু)

নিচে আমরা ফাইল ধরে ধরে function/important property explain করছি:

- এটা কী কাজ করে
- input কী নেয়
- output কী দেয়
- ভিতরে কীভাবে কাজ করে
- কেন দরকার

### 9.1) KUET_TradeApp.swift

#### A) `application(_:didFinishLaunchingWithOptions:)`

**কোথায়:** `AppDelegate` class এর ভিতরে

**কাজ কী:**

- অ্যাপ চালু হওয়ার একদম শুরুতে Firebase initialize করে

**Input:**

- `application`: current UIApplication instance
- `launchOptions`: app launch context (notification/deep link ইত্যাদি, optional)

**Output:**

- `Bool` রিটার্ন করে
- `true` মানে launch setup সফল

**ভিতরে কীভাবে কাজ করে:**

1. `FirebaseApp.configure()` call হয়
2. Firebase config file (`GoogleService-Info.plist`) থেকে সেটিং পড়ে
3. Auth/Firestore/Storage use করার জন্য app প্রস্তুত হয়
4. শেষে `true` return হয়

**কেন দরকার:**

- এটা না করলে Firebase service call করার সময় app crash/failed হতে পারে

---

#### B) `var body: some Scene` (in `KUET_TradeApp`)

**কাজ কী:**

- অ্যাপের root scene define করে

**Input:**

- direct parameter নেয় না

**Output:**

- `some Scene` (এখানে `WindowGroup`)

**ভিতরে কীভাবে কাজ করে:**

1. `WindowGroup` তৈরি করে
2. প্রথম root view হিসেবে `ContentView()` inject করে
3. এখান থেকেই app UI flow শুরু হয়

**কেন দরকার:**

- SwiftUI app lifecycle এ এটা মূল entry UI point

---

#### C) `@UIApplicationDelegateAdaptor(AppDelegate.self) var delegate`

**এটা function না, property-wrapper based bridge**

**কাজ কী:**

- SwiftUI lifecycle এর সাথে UIKit `AppDelegate` যুক্ত করে

**Input:**

- `AppDelegate.self` type

**Output:**

- runtime এ `AppDelegate` instance manage হয়

**কেন দরকার:**

- Firebase configure করার কাজটা ঐ delegate launch method এ চালানোর জন্য

---

### 9.2) ContentView.swift

#### A) `@StateObject private var authViewModel = AuthViewModel()`

**এটা function না, state owner property**

**কাজ কী:**

- `AuthViewModel`-এর lifecycle `ContentView` level এ hold করে

**Input:**

- `AuthViewModel()` initializer

**Output:**

- observable object instance

**ভিতরে কীভাবে কাজ করে:**

1. View প্রথমবার তৈরি হলে `AuthViewModel` create হয়
2. পরে view redraw হলেও একই instance ধরে রাখে
3. auth state change হলে UI re-render হয়

**কেন দরকার:**

- auth state app-wide gate হিসেবে কাজ করে, তাই stable instance লাগবে

---

#### B) `var body: some View`

**কাজ কী:**

- auth state অনুযায়ী কোন screen দেখাবে তা ঠিক করে

**Input:**

- direct function input নেই
- internally `authViewModel.isCheckingAuth`, `authViewModel.isLoggedIn` read করে

**Output:**

- `some View` (LaunchScreenView / MainTabView / LoginView)

**ভিতরে কীভাবে কাজ করে:**

1. `isCheckingAuth == true` হলে `LaunchScreenView()` দেখায়
2. না হলে `isLoggedIn == true` হলে `MainTabView(authViewModel: authViewModel)` দেখায়
3. অন্যথায় `LoginView(viewModel: authViewModel)` দেখায়
4. দুইটা `.animation(...)` দিয়ে state switch smooth করে

**কেন দরকার:**

- এই ফাইলটাই app-এর authentication gatekeeper

---

#### C) `.animation(.easeInOut(duration: 0.4), value: ...)`

**এটা modifier, pure function না**

**কাজ কী:**

- auth state change হলে screen transition smoother করে

**Input:**

- animation curve (`easeInOut`, `0.4s`)
- observed value (`isLoggedIn`, `isCheckingAuth`)

**Output:**

- animated view transitions

**ভিতরে কীভাবে কাজ করে:**

1. observed value change detect করে
2. নতুন view render animation সহ করে

**কেন দরকার:**

- হঠাৎ screen switch না হয়ে polished UX দেয়

---

### 9.3) Mini Data Flow (এই দুই ফাইল মিলিয়ে)

1. App start -> `application(_:didFinishLaunchingWithOptions:)` -> Firebase setup
2. `KUET_TradeApp.body` -> `ContentView()` root হিসেবে render
3. `ContentView` -> auth checking state দেখে launch অথবা login/main tabs দেখায়
4. user login করলে একই `authViewModel` main tabs-এ pass হয়

---

### 9.4) Viva/Defense Ready Questions (এই অংশ থেকে)

1. কেন `@StateObject` ব্যবহার করা হয়েছে, `@ObservedObject` না?
2. Firebase configure কোথায় হচ্ছে এবং কেন launch phase-এ?
3. `ContentView`-কে কেন gatekeeper বলা হয়?
4. `isCheckingAuth` আর `isLoggedIn` আলাদা state রাখার সুবিধা কী?
5. animation modifiers না দিলে UX-এ কী পরিবর্তন হবে?

---

### 9.5) Progress Update

- [x] KUET_TradeApp.swift full explanation (function-level)
- [x] ContentView.swift full explanation (function-level)
- [x] MainTabView.swift full explanation (function-level)
- [ ] পরবর্তী: AuthViewModel.swift function-by-function

---

### 9.6) MainTabView.swift

#### A) `@ObservedObject var authViewModel: AuthViewModel`

**এটা function না, injected observable dependency**

**কাজ কী:**

- parent (`ContentView`) থেকে আসা auth state ব্যবহার করা

**Input:**

- `AuthViewModel` instance (constructor দিয়ে pass হয়)

**Output:**

- direct value return করে না; UI update trigger করে

**ভিতরে কীভাবে কাজ করে:**

1. logged-in user related data এখানে observable হিসেবে থাকে
2. `ProfileView` ও `MyAdsView`-এ এই object pass হয়

**কেন দরকার:**

- tabগুলোর মধ্যে consistent auth/user state রাখতে

---

#### B) `@StateObject private var itemViewModel = ItemViewModel()`

**এটা function না, local state owner**

**কাজ কী:**

- item data/search/filter state একবার create করে সব tab-এ share করা

**Input:**

- `ItemViewModel()` initializer

**Output:**

- shared observable state for Home/Post/MyAds tabs

**ভিতরে কীভাবে কাজ করে:**

1. MainTabView create হলে ItemViewModel তৈরি হয়
2. HomeView, PostItemView, MyAdsView এই একই instance use করে
3. ফলে tab change করলেও filter/data state continuity থাকে

**কেন দরকার:**

- প্রতিটা tab-এ আলাদা item state না করে single source of truth রাখা

---

#### C) `@StateObject private var networkMonitor = NetworkMonitor.shared`

**এটা singleton monitor bind করার state object**

**কাজ কী:**

- internet connection status observe করা

**Input:**

- `NetworkMonitor.shared`

**Output:**

- `isConnected` change হলে UI update

**কেন দরকার:**

- offline banner reactive ভাবে show/hide করার জন্য

---

#### D) `@State private var selectedTab: Int = 0`

**এটা selected tab index state**

**কাজ কী:**

- বর্তমানে কোন tab active তা track করা

**Input:**

- user tab tap করলে selection change হয়

**Output:**

- TabView selected page change

**কেন দরকার:**

- tab switch event detect করে haptic feedback দিতে

---

#### E) `var body: some View`

**কাজ কী:**

- main app shell (offline banner + tab navigation) render করা

**Input:**

- internal states: `networkMonitor.isConnected`, `selectedTab`
- dependencies: `authViewModel`, `itemViewModel`

**Output:**

- `some View` (VStack containing OfflineBanner + TabView)

**ভিতরে কীভাবে কাজ করে:**

1. উপরে `OfflineBannerView()` রাখে
2. banner-এ `.animation(..., value: networkMonitor.isConnected)` apply করে
3. নিচে `TabView(selection: $selectedTab)` তৈরি করে
4. চারটি tab define করে:

- `HomeView(itemViewModel: itemViewModel)` tag `0`
- `PostItemView(itemViewModel: itemViewModel)` tag `1`
- `MyAdsView(authViewModel: authViewModel, itemViewModel: itemViewModel)` tag `2`
- `ProfileView(authViewModel: authViewModel)` tag `3`

5. `.onChange(of: selectedTab)` এ light haptic trigger করে

**কেন দরকার:**

- login-এর পর পুরো app navigation experience এই screen থেকে control হয়

---

#### F) `.onChange(of: selectedTab) { _, _ in ... }`

**এটা event handler closure**

**কাজ কী:**

- tab পরিবর্তনের সাথে সাথে tactile feedback দেওয়া

**Input:**

- old এবং new tab value (এখানে use করা হয়নি)

**Output:**

- visible return নেই; side effect: haptic vibration

**ভিতরে কীভাবে কাজ করে:**

1. `UIImpactFeedbackGenerator(style: .light)` বানায়
2. `impactOccurred()` call করে

**কেন দরকার:**

- UI interaction feel improve করে

---

#### G) `PlaceholderTabView` (supporting view)

**এটা optional reusable placeholder component**

**কাজ কী:**

- future/empty tabs দ্রুত দেখানোর scaffold

**Important members:**

- `icon`, `title`, `subtitle`: display content
- `showSignOut`: sign-out button দেখাবে কি না
- `onSignOut`: button action callback
- `var body: some View`: static placeholder UI render

**কেন দরকার:**

- development phase-এ unfinished tab এর জন্য দ্রুত UI fallback

---

### 9.7) Mini Data Flow (MainTabView)

1. ContentView থেকে `authViewModel` inject হয়
2. MainTabView নিজে `itemViewModel` create করে এবং 3 tab-এ share করে
3. Home/Post/MyAds একই item source use করে
4. tab change হলে `selectedTab` update + haptic হয়
5. network offline হলে top banner animate হয়ে দেখায়

---

### 9.8) Viva/Defense Ready Questions (MainTabView)

1. কেন `itemViewModel` কে MainTabView level-এ রাখা হয়েছে?
2. HomeView/PostItemView/MyAdsView এর মধ্যে state sharing কীভাবে হচ্ছে?
3. `@ObservedObject` vs `@StateObject` এখানে কেন আলাদা?
4. `selectedTab` track না করলে কোন behavior হারাবে?
5. OfflineBannerView-এ animation value-based কেন?

---

### 9.9) AuthViewModel.swift

এই ফাইল হলো authentication-এর brain। Login/Signup/Forgot Password/Sign Out + error handling + form validation সব এখানে।

#### A) `static let shared = AuthViewModel()`

**কাজ কী:**

- shared singleton access দেয়

**Input:**

- direct input নেই

**Output:**

- globally reusable `AuthViewModel` instance

**কেন দরকার:**

- কিছু জায়গায় (যেমন post flow) current user দ্রুত access করতে

---

#### B) `init()`

**কাজ কী:**

- object create হওয়ার সাথে সাথে auth listener start করে

**Input:**

- নেই

**Output:**

- object initialized state

**ভিতরে কীভাবে কাজ করে:**

1. `listenToAuthState()` call করে
2. Firebase auth state change observe করা শুরু হয়

---

#### C) `deinit`

**কাজ কী:**

- object destroy হওয়ার সময় auth listener remove করা

**Input:**

- নেই

**Output:**

- listener cleanup

**কেন দরকার:**

- memory leak বা duplicate listener avoid করতে

---

#### D) `private func listenToAuthState()`

**কাজ কী:**

- Firebase login/logout state observe করে local state update করা

**Input:**

- direct input নেই

**Output:**

- return কিছু দেয় না; side effect হিসেবে `isLoggedIn`, `isCheckingAuth`, `currentUser` update হয়

**ভিতরে কীভাবে কাজ করে:**

1. `AuthService.shared.addAuthStateListener` register করে
2. callback-এ `loggedIn` value পায়
3. main actor task এ `isLoggedIn` set করে
4. auth check শেষ হলে `isCheckingAuth = false`
5. logged in হলে `fetchUser()` call
6. logged out হলে `currentUser = nil`

---

#### E) `func fetchUser() async`

**কাজ কী:**

- current user profile Firestore থেকে fetch করা

**Input:**

- direct parameter নেই

**Output:**

- direct return নেই; `currentUser` update হয়

**ভিতরে কীভাবে কাজ করে:**

1. `AuthService.shared.fetchCurrentUser()` call করে
2. success হলে `currentUser` set
3. fail হলে fallback path চলে:

- Firebase Auth এর raw user থেকে `KTUser` বানায়
- minimal data দিয়েও app usable রাখে

4. error console-এ print করে

**কেন দরকার:**

- Firestore profile না পেলেও app crash না করে graceful degrade করে

---

#### F) `func login() async`

**কাজ কী:**

- email/password দিয়ে user sign in করা

**Input:**

- `loginEmail`, `loginPassword` (stored state fields)

**Output:**

- direct return নেই; success হলে auth listener state update করে

**ভিতরে কীভাবে কাজ করে:**

1. `validateLoginFields()` pass না করলে return
2. `isLoading = true`
3. `AuthService.shared.signIn(...)` call
4. success হলে `clearLoginFields()`
5. fail হলে `mapAuthError(error)` + `showErrorMessage(...)`
6. শেষে `isLoading = false`

---

#### G) `func signUp() async`

**কাজ কী:**

- নতুন user account create করা এবং profile save করা

**Input:**

- signup form fields (`signupName`, `signupEmail`, `signupPhone`, `signupDepartment`, `signupPassword`)

**Output:**

- direct return নেই; `currentUser` set হতে পারে

**ভিতরে কীভাবে কাজ করে:**

1. `validateSignupFields()` check
2. `isLoading = true`
3. `AuthService.shared.signUp(...)` call
4. success হলে returned user `currentUser`-এ set
5. `clearSignupFields()`
6. error হলে mapped message show
7. শেষে `isLoading = false`

---

#### H) `func resetPassword() async`

**কাজ কী:**

- forgot-password email পাঠানো

**Input:**

- `resetEmail`

**Output:**

- success হলে `resetEmailSent = true`

**ভিতরে কীভাবে কাজ করে:**

1. email trim করে
2. empty হলে error show
3. invalid format হলে error show
4. valid হলে `AuthService.shared.resetPassword(email:)`
5. success হলে UI success state (`resetEmailSent`) set

---

#### I) `func signOut()`

**কাজ কী:**

- current session logout করা

**Input:**

- নেই

**Output:**

- direct return নেই; local state clear হয়

**ভিতরে কীভাবে কাজ করে:**

1. `AuthService.shared.signOut()` try করে
2. success হলে `currentUser = nil`
3. login/signup form fields clear
4. fail হলে error message show

---

#### J) `private func validateLoginFields() -> Bool`

**কাজ কী:**

- login input valid কিনা check করা

**Input:**

- `loginEmail`, `loginPassword`

**Output:**

- `true` = valid, `false` = invalid

**Validation rules:**

1. email/password empty না
2. email valid format
3. password min length (`AppConstants.Validation.minPasswordLength`)

---

#### K) `private func validateSignupFields() -> Bool`

**কাজ কী:**

- signup form সব input verify করা

**Input:**

- সব signup fields

**Output:**

- `Bool`

**Validation rules:**

1. সব mandatory field non-empty
2. valid email
3. valid phone (10–14 digits rule)
4. password minimum length
5. password এবং confirm password same

---

#### L) `private func showErrorMessage(_ message: String)`

**কাজ কী:**

- UI alert state এক জায়গা থেকে set করা

**Input:**

- `message: String`

**Output:**

- direct return নেই; `errorMessage` এবং `showError` update হয়

---

#### M) `private func mapAuthError(_ error: Error) -> String`

**কাজ কী:**

- Firebase auth error code কে user-friendly message-এ convert করা

**Input:**

- `Error`

**Output:**

- `String` (displayable message)

**ভিতরে কীভাবে কাজ করে:**

1. `NSError` এ cast করে
2. domain `AuthErrorDomain` কিনা check করে
3. `AuthErrorCode` switch করে readable message return করে
4. unknown হলে `localizedDescription`

---

#### N) `private func clearLoginFields()`

**কাজ কী:**

- login form reset করা

**Input:**

- নেই

**Output:**

- `loginEmail = ""`, `loginPassword = ""`

---

#### O) `private func clearSignupFields()`

**কাজ কী:**

- signup form reset করা

**Input:**

- নেই

**Output:**

- signup সম্পর্কিত সব field empty string

---

#### P) `func clearResetFields()`

**কাজ কী:**

- forgot-password screen state reset করা

**Input:**

- নেই

**Output:**

- `resetEmail = ""`
- `resetEmailSent = false`

---

### 9.10) Mini Data Flow (AuthViewModel)

1. `init()` -> `listenToAuthState()` শুরু
2. user login/signup করলে service call হয়
3. Firebase auth state বদলালে listener `isLoggedIn` update করে
4. logged in হলে `fetchUser()` profile আনে
5. validation fail বা service fail হলে `showErrorMessage()` alert state set করে

---

### 9.11) Viva/Defense Ready Questions (AuthViewModel)

1. `login()` success হলে কেন সাথে সাথে `isLoggedIn = true` set করা হয়নি?
2. `fetchUser()`-এ fallback user তৈরির প্রয়োজন কেন?
3. `mapAuthError()` না থাকলে UX-এ কী সমস্যা হতো?
4. `validateSignupFields()`-এ কোন ruleগুলো business rule হিসেবে ধরা হয়েছে?
5. `deinit`-এ listener remove করা কেন গুরুত্বপূর্ণ?

---

### 9.12) Progress Update

- [x] KUET_TradeApp.swift full explanation (function-level)
- [x] ContentView.swift full explanation (function-level)
- [x] MainTabView.swift full explanation (function-level)
- [x] AuthViewModel.swift full explanation (function-level)
- [x] AuthService.swift full explanation (function-level)
- [ ] পরবর্তী: FirestoreService.swift function-by-function

---

### 9.13) AuthService.swift

এই ফাইলটি Firebase Auth + Firestore user document-এর low-level service layer।
AuthViewModel এই service call করে authentication কাজ সম্পন্ন করে।

#### A) `static let shared = AuthService()`

**কাজ কী:**

- singleton service instance দেয়

**Input:**

- direct input নেই

**Output:**

- globally reusable `AuthService` object

**কেন দরকার:**

- app জুড়ে একই auth/db handle ব্যবহার করতে

---

#### B) `private init() {}`

**কাজ কী:**

- বাইরের code যেন নতুন instance বানাতে না পারে

**Input/Output:**

- direct কিছু নেই

**কেন দরকার:**

- singleton pattern enforce করতে

---

#### C) `var currentUserID: String?`

**এটা computed property**

**কাজ কী:**

- current logged-in user-এর UID return করা

**Input:**

- নেই

**Output:**

- `String?` (logged in না থাকলে `nil`)

**ভিতরে কীভাবে কাজ করে:**

1. `auth.currentUser?.uid` read করে
2. optional UID return করে

---

#### D) `var isLoggedIn: Bool`

**এটা computed property**

**কাজ কী:**

- user logged in আছে কি না quick check

**Input:**

- নেই

**Output:**

- `Bool`

**ভিতরে কীভাবে কাজ করে:**

1. `auth.currentUser != nil` evaluate করে
2. true/false return করে

---

#### E) `func signUp(name:email:phone:department:password:) async throws -> KTUser`

**কাজ কী:**

- নতুন user account create করে
- Firebase Auth profile update করে
- Firestore-এ user document save করে

**Input:**

- `name: String`
- `email: String`
- `phone: String`
- `department: String`
- `password: String`

**Output:**

- success হলে `KTUser`
- failure হলে `throws`

**ভিতরে কীভাবে কাজ করে:**

1. `auth.createUser(withEmail:password:)` দিয়ে auth account create
2. returned `uid` নেয়
3. `createProfileChangeRequest()` দিয়ে Firebase Auth profile-এর displayName set
4. `commitChanges()` call করে profile update persist করে
5. local `KTUser` object বানায়
6. `db.collection("users").document(uid).setData(from: newUser)` দিয়ে Firestore-এ save করে
7. `newUser` return করে

**কেন দরকার:**

- শুধু Auth account না, app-এর own user profile dataও একই সাথে persist করতে

---

#### F) `func signIn(email:password:) async throws`

**কাজ কী:**

- existing user login করা

**Input:**

- `email: String`
- `password: String`

**Output:**

- direct return নেই (`Void`)
- fail হলে `throws`

**ভিতরে কীভাবে কাজ করে:**

1. `auth.signIn(withEmail:password:)` call
2. success হলে Firebase currentUser set হয়
3. এরপর listener (viewmodel side) auth state update handle করে

---

#### G) `func signOut() throws`

**কাজ কী:**

- current user logout করা

**Input:**

- নেই

**Output:**

- direct return নেই
- fail হলে `throws`

**ভিতরে কীভাবে কাজ করে:**

1. `auth.signOut()` call
2. success হলে current session clear

---

#### H) `func resetPassword(email:) async throws`

**কাজ কী:**

- password reset email trigger করা

**Input:**

- `email: String`

**Output:**

- direct return নেই
- fail হলে `throws`

**ভিতরে কীভাবে কাজ করে:**

1. `auth.sendPasswordReset(withEmail:)` call
2. Firebase ঐ email-এ reset link পাঠায়

---

#### I) `func fetchCurrentUser() async throws -> KTUser?`

**কাজ কী:**

- Firestore থেকে logged-in user profile document fetch করা

**Input:**

- direct parameter নেই

**Output:**

- `KTUser?`
- logged in না থাকলে `nil`
- firestore/decode fail হলে `throws`

**ভিতরে কীভাবে কাজ করে:**

1. `currentUserID` guard করে UID নেয়
2. `users/{uid}` document fetch করে
3. `snapshot.data(as: KTUser.self)` দিয়ে decode করে
4. decoded user return করে

---

#### J) `func addAuthStateListener(completion:) -> AuthStateDidChangeListenerHandle`

**কাজ কী:**

- auth state change observer register করা

**Input:**

- `completion: (Bool) -> Void`

**Output:**

- `AuthStateDidChangeListenerHandle` (পরে remove করার জন্য)

**ভিতরে কীভাবে কাজ করে:**

1. `auth.addStateDidChangeListener` register করে
2. Firebase user nil/non-nil দেখে `completion(user != nil)` call করে

**কেন দরকার:**

- UI-তে realtime login/logout gate switch করতে

---

#### K) `func removeAuthStateListener(_ handle:)`

**কাজ কী:**

- previously added auth listener remove করা

**Input:**

- `handle: AuthStateDidChangeListenerHandle`

**Output:**

- direct return নেই

**ভিতরে কীভাবে কাজ করে:**

1. `auth.removeStateDidChangeListener(handle)` call করে

---

### 9.14) Mini Data Flow (AuthService)

1. Signup: `createUser` -> profile displayName update -> Firestore user doc save
2. Login: `signIn` -> Firebase currentUser set -> listener callback -> UI state update
3. Logout: `signOut` -> listener callback -> app login screen এ ফিরে যায়
4. Profile load: `fetchCurrentUser` -> `users/{uid}` fetch -> decode `KTUser`

---

### 9.15) Viva/Defense Ready Questions (AuthService)

1. কেন signup-এর সময় Auth + Firestore দুই জায়গায় data save করা হয়?
2. `currentUserID` nil হলে `fetchCurrentUser()`-এ কী হবে?
3. listener handle return করা কেন দরকার?
4. `signIn()` method কেন user object return করছে না?
5. Firebase Auth profile আর Firestore user profile-এর মধ্যে পার্থক্য কী?

---

### 9.16) FirestoreService.swift

এই ফাইলটি items collection-এর CRUD এবং listing query logic handle করে।
ItemViewModel, MyAdsView, Post/Edit flow এই service-এর উপর নির্ভর করে।

#### A) `static let shared = FirestoreService()`

**কাজ কী:**

- singleton instance provide করা

**Input:**

- নেই

**Output:**

- global `FirestoreService` object

---

#### B) `private init() {}`

**কাজ কী:**

- singleton enforce করা

**Input/Output:**

- direct কিছু নেই

---

#### C) `private var itemsCollection: CollectionReference`

**এটা computed property**

**কাজ কী:**

- Firestore-এর items collection reference reuse করা

**Input:**

- নেই

**Output:**

- `CollectionReference` (`db.collection("items")`)

**কেন দরকার:**

- বারবার hardcoded path না লিখে centralized reference রাখা

---

#### D) `func createItem(_ item: Item) async throws -> String`

**কাজ কী:**

- নতুন item document তৈরি করা

**Input:**

- `item: Item`

**Output:**

- success হলে created document ID (`String`)
- fail হলে `throws`

**ভিতরে কীভাবে কাজ করে:**

1. `itemsCollection.addDocument(from: item)` call করে
2. Firestore document তৈরি হয়
3. `documentID` return করে

---

#### E) `func fetchAllItems() async throws -> [Item]`

**কাজ কী:**

- সব item fetch করে available item list return করা

**Input:**

- নেই

**Output:**

- `[Item]`

**ভিতরে কীভাবে কাজ করে:**

1. `itemsCollection.getDocuments()` থেকে snapshot আনে
2. প্রতিটি doc `Item`-এ decode করার চেষ্টা করে (`compactMap`)
3. `isAvailable == true` item filter করে
4. `createdAt` descending sort করে return দেয়

**নোট:**

- filter/sort client-side করা হচ্ছে

---

#### F) `func fetchItems(byCategory:) async throws -> [Item]`

**কাজ কী:**

- নির্দিষ্ট category-এর items আনা

**Input:**

- `category: ItemCategory`

**Output:**

- `[Item]`

**ভিতরে কীভাবে কাজ করে:**

1. Firestore query: `whereField("category", isEqualTo: category.rawValue)`
2. documents decode করে
3. available item filter করে
4. newest-first sort করে return দেয়

---

#### G) `func fetchUserItems(userID:) async throws -> [Item]`

**কাজ কী:**

- নির্দিষ্ট seller/user-এর সব ad আনা (My Ads এর জন্য)

**Input:**

- `userID: String`

**Output:**

- `[Item]`

**ভিতরে কীভাবে কাজ করে:**

1. query: `whereField("sellerID", isEqualTo: userID)`
2. decode করে item list তৈরি
3. created date descending sort
4. return

**নোট:**

- এখানে sold+active দুটোই আসে, যাতে seller manage করতে পারে

---

#### H) `func fetchItem(byID:) async throws -> Item?`

**কাজ কী:**

- single item details fetch করা

**Input:**

- `id: String` (document ID)

**Output:**

- `Item?`

**ভিতরে কীভাবে কাজ করে:**

1. `itemsCollection.document(id).getDocument()`
2. document data `Item`-এ decode
3. decoded object return

---

#### I) `func updateItem(_ item:) async throws`

**কাজ কী:**

- existing item document update করা

**Input:**

- `item: Item` (must include `id`)

**Output:**

- direct return নেই
- fail হলে `throws`

**ভিতরে কীভাবে কাজ করে:**

1. `item.id` guard করে
2. id না থাকলে `FirestoreError.missingID` throw
3. `setData(from: item, merge: true)` দিয়ে update

**কেন merge true:**

- document overwrite না করে fields update preserve করতে

---

#### J) `func deleteItem(byID:) async throws`

**কাজ কী:**

- item document delete করা

**Input:**

- `id: String`

**Output:**

- direct return নেই

**ভিতরে কীভাবে কাজ করে:**

1. `itemsCollection.document(id).delete()` call

---

#### K) `func toggleAvailability(itemID:isAvailable:) async throws`

**কাজ কী:**

- item active/sold status toggle করা

**Input:**

- `itemID: String`
- `isAvailable: Bool`

**Output:**

- direct return নেই

**ভিতরে কীভাবে কাজ করে:**

1. target document select করে
2. `updateData` দিয়ে দুই field update:

- `isAvailable`
- `updatedAt = Timestamp(date: Date())`

**কেন দরকার:**

- My Ads থেকে mark sold/relist action support করার জন্য

---

#### L) `enum FirestoreError: LocalizedError`

**কাজ কী:**

- service-level custom error type define করা

**Cases:**

- `missingID`
- `encodingFailed`
- `decodingFailed`

---

#### M) `var errorDescription: String?`

**কাজ কী:**

- custom error-এর জন্য readable message return করা

**Input:**

- current enum case

**Output:**

- `String?` user-friendly error text

---

### 9.17) Mini Data Flow (FirestoreService)

1. Post flow -> `createItem` -> নতুন doc তৈরি
2. Home flow -> `fetchAllItems` -> available items list
3. My Ads flow -> `fetchUserItems` -> seller-specific list
4. Edit flow -> `updateItem`
5. Delete flow -> `deleteItem`
6. Sold/Relist flow -> `toggleAvailability`

---

### 9.18) Viva/Defense Ready Questions (FirestoreService)

1. `fetchAllItems()`-এ filtering/sorting client-side করার impact কী?
2. `updateItem()`-এ `merge: true` কেন ব্যবহার করা হয়েছে?
3. `fetchUserItems()` কেন sold items-ও return করে?
4. `toggleAvailability()`-এ `updatedAt` update করা কেন দরকার?
5. custom `FirestoreError` কখন কাজে লাগে?

---

### 9.19) Progress Update

- [x] KUET_TradeApp.swift full explanation (function-level)
- [x] ContentView.swift full explanation (function-level)
- [x] MainTabView.swift full explanation (function-level)
- [x] AuthViewModel.swift full explanation (function-level)
- [x] AuthService.swift full explanation (function-level)
- [x] FirestoreService.swift full explanation (function-level)
- [x] StorageService.swift full explanation (function-level)
- [x] ItemViewModel.swift full explanation (function-level)
- [ ] পরবর্তী: PostItemViewModel.swift function-by-function

---

### 9.20) StorageService.swift

এই ফাইল image upload/delete সম্পর্কিত Firebase Storage operations handle করে।
PostItemViewModel ও Edit flow এই service ব্যবহার করে।

#### A) `static let shared = StorageService()`

**কাজ কী:**

- singleton storage service instance দেয়

**Input/Output:**

- direct input নেই, global `StorageService` object দেয়

---

#### B) `private init() {}`

**কাজ কী:**

- singleton enforce করা

---

#### C) `func uploadImage(_ image:path:) async throws -> String`

**কাজ কী:**

- single image upload করে downloadable URL return করা

**Input:**

- `image: UIImage`
- `path: String` (storage path)

**Output:**

- success হলে `String` download URL
- fail হলে `throws`

**ভিতরে কীভাবে কাজ করে:**

1. `image.jpegData(compressionQuality: 0.5)` দিয়ে compress করে
2. compression fail হলে `StorageError.compressionFailed`
3. `storage.reference().child(path)` reference তৈরি করে
4. metadata contentType `image/jpeg` set করে
5. `putDataAsync` দিয়ে upload করে
6. `downloadURL()` নিয়ে absolute string return করে

**কেন দরকার:**

- Firestore-এ image binary না রেখে lightweight URL save করতে

---

#### D) `func uploadImages(_ images:folderPath:) async throws -> [String]`

**কাজ কী:**

- multiple image sequentially upload করা

**Input:**

- `images: [UIImage]`
- `folderPath: String`

**Output:**

- `[String]` (সব uploaded image URL)

**ভিতরে কীভাবে কাজ করে:**

1. empty `urls` array নেয়
2. loop-এ প্রতিটি image এর জন্য unique path বানায়:
   - `image_<index>_<uuid>.jpg`
3. internal `uploadImage(...)` call করে
4. পাওয়া URL array-তে append করে
5. শেষে URLs return

**নোট:**

- sequential upload হওয়ায় code সহজ, তবে অনেক image হলে একটু সময় বেশি লাগতে পারে

---

#### E) `func deleteImage(url:) async throws`

**কাজ কী:**

- single image URL থেকে storage object delete করা

**Input:**

- `url: String`

**Output:**

- direct return নেই

**ভিতরে কীভাবে কাজ করে:**

1. `storage.reference(forURL: url)` থেকে reference নেয়
2. `ref.delete()` call করে

---

#### F) `func deleteImages(urls:) async throws`

**কাজ কী:**

- multiple images delete করা

**Input:**

- `urls: [String]`

**Output:**

- direct return নেই

**ভিতরে কীভাবে কাজ করে:**

1. loop করে প্রতিটি URL-এ `deleteImage(url:)` call
2. যেকোন delete fail হলে throw হতে পারে

---

#### G) `enum StorageError: LocalizedError`

**কাজ কী:**

- custom storage-related error cases define করা

**Cases:**

- `compressionFailed`
- `uploadFailed`
- `downloadURLFailed`

---

#### H) `var errorDescription: String?`

**কাজ কী:**

- error case অনুযায়ী readable message return করা

**Output:**

- optional readable string

---

### 9.21) Mini Data Flow (StorageService)

1. Post/Edit form থেকে images আসে
2. `uploadImages` -> প্রতিটি image upload -> URL list
3. URL list Firestore item document-এ save হয়
4. Edit/Delete এ removed image URL থাকলে `deleteImages` run হয়

---

### 9.22) Viva/Defense Ready Questions (StorageService)

1. কেন image compress করে upload করা হচ্ছে?
2. URL-based storage design-এর সুবিধা কী?
3. upload sequence parallel না হওয়ায় trade-off কী?
4. delete করার সময় URL reference কেন দরকার?
5. StorageError cases কোন কোন scenario cover করে?

---

### 9.23) ItemViewModel.swift

এই ফাইল Home listing, filter, search, sort এবং refresh state control করে।

#### A) `init()`

**কাজ কী:**

- view model তৈরি হলেই initial item load trigger করা

**Input:**

- নেই

**Output:**

- direct return নেই

**ভিতরে কীভাবে কাজ করে:**

1. `Task { await loadItems() }` run করে
2. asynchronous ভাবে data fetch শুরু হয়

---

#### B) `func loadItems() async`

**কাজ কী:**

- backend থেকে items load করে local state-এ রাখা

**Input:**

- নেই

**Output:**

- direct return নেই
- side effect: `allItems`, `filteredItems`, loading/error flags update

**ভিতরে কীভাবে কাজ করে:**

1. `isLoading = allItems.isEmpty` (first load-এ skeleton দেখানোর জন্য)
2. `FirestoreService.shared.fetchAllItems()` call
3. success হলে `allItems = items`
4. `applyFilters()` run করে filtered list build
5. fail হলে `errorMessage` set + `showError = true`
6. শেষে `isLoading = false`, `isRefreshing = false`

---

#### C) `func refresh() async`

**কাজ কী:**

- pull-to-refresh logic চালানো

**Input:**

- নেই

**Output:**

- direct return নেই

**ভিতরে কীভাবে কাজ করে:**

1. `isRefreshing = true`
2. `loadItems()` call করে

---

#### D) `func applyFilters()`

**কাজ কী:**

- category/search/price/sort apply করে final list তৈরি করা

**Input:**

- internal states:
  - `allItems`
  - `selectedCategory`
  - `searchText`
  - `minPrice`, `maxPrice`
  - `selectedSort`

**Output:**

- `filteredItems` update

**ভিতরে কীভাবে কাজ করে:**

1. `result = allItems`
2. category selected থাকলে filter
3. search text থাকলে title/description/seller/category-তে case-insensitive match
4. min/max price parse করে range filter
5. selected sort অনুযায়ী sort
6. `filteredItems = result`

**কেন দরকার:**

- UI থেকে filter state change হলেই centralized logic চালাতে

---

#### E) `func clearFilters()`

**কাজ কী:**

- সব filter default state-এ reset করা

**Input:**

- নেই

**Output:**

- filter states reset (search/category/sort/price)

**ভিতরে কীভাবে কাজ করে:**

1. `searchText = ""`
2. `selectedCategory = nil`
3. `selectedSort = .newest`
4. `minPrice = ""`, `maxPrice = ""`

**নোট:**

- যেহেতু didSet-এ `applyFilters()` আছে, state change হলেই list auto-update হয়

---

#### F) `var hasActiveFilters: Bool`

**কাজ কী:**

- কোনো filter active আছে কি না check করা

**Input:**

- current filter states

**Output:**

- `Bool`

---

#### G) `var activeFilterCount: Int`

**কাজ কী:**

- মোট কয় ধরনের filter active তা count করা

**Input:**

- filter states

**Output:**

- `Int`

**কেন দরকার:**

- UI badge-এ active filter count দেখাতে

---

#### H) `var itemCount: Int`

**কাজ কী:**

- filtered item count return করা

**Output:**

- `Int` (`filteredItems.count`)

---

#### I) `var isEmpty: Bool`

**কাজ কী:**

- empty state দেখাবে কি না নির্ধারণ করা

**Output:**

- `Bool` (`filteredItems.isEmpty && !isLoading`)

---

#### J) `var priceRangeDescription: String?`

**কাজ কী:**

- min/max price filter কে human-readable label বানানো

**Input:**

- `minPrice`, `maxPrice`

**Output:**

- `String?` যেমন:
  - `৳200 – ৳500`
  - `৳500+`
  - `Up to ৳300`
  - না থাকলে `nil`

---

#### K) Filter didSet triggers (`searchText`, `selectedCategory`, `selectedSort`, `minPrice`, `maxPrice`)

**এগুলো function না, reactive hooks**

**কাজ কী:**

- filter field পরিবর্তনের সাথে সাথে `applyFilters()` auto run

**কেন দরকার:**

- আলাদা apply button ছাড়াই live filtering UX পেতে

---

### 9.24) Mini Data Flow (ItemViewModel)

1. init -> `loadItems()`
2. `allItems` fetch হওয়ার পর `applyFilters()` run
3. UI-তে filter field change -> didSet -> `applyFilters()`
4. final list `filteredItems` এ যায়
5. UI `itemCount`, `hasActiveFilters`, `isEmpty` ব্যবহার করে render করে

---

### 9.25) Viva/Defense Ready Questions (ItemViewModel)

1. filter fields-এ didSet ব্যবহার করার সুবিধা কী?
2. `isLoading = allItems.isEmpty` logic কেন useful?
3. `allItems` আর `filteredItems` দুটো list রাখার কারণ কী?
4. client-side filter/sort এর সীমাবদ্ধতা কী?
5. `isEmpty`-তে `!isLoading` condition কেন দরকার?

---

### 9.26) PostItemViewModel.swift

এই ফাইল নতুন item post এবং existing item edit করার form state control করে।

#### A) Form Fields

```swift
@Published var title, description, priceText, selectedCategory, selectedImages
@Published var isLoading, errorMessage, showError
@Published var didPostSuccessfully, didEditSuccessfully
```

**কাজ:** নতুন/edit item form-এর সব state রাখা।

---

#### B) `func loadItem(_ item: Item)`

**কাজ কী:** edit mode-এ existing item data form field-এ load করা।

**ভিতরে:** `title`, `description`, `priceText`, `category` copy করা + `existingImageURLs` store করা।

---

#### C) `func addImage(_ image: UIImage)`

**কাজ কী:** নতুন image list-এ add করা।

**Check:** `canAddMoreImages` (max limit check)।

**Side effect:** `selectedImages` append।

---

#### D) `func removeImage(at index: Int)` & `func removeExistingImage(at index: Int)`

**কাজ কী:** নতুন বা পুরনো image remove করা।

**ভিতরে:** bounds check করে index-এ remove করা।

---

#### E) `func validate() -> Bool`

**কাজ কী:** title, description, price, image সব field validate করা।

**Check করে:**

- title empty/too long
- description empty/too long
- price valid এবং positive
- image count >= 1 (post mode)

**Return:** সব valid হলে `true`, else `false` + showErrorMessage।

---

#### F) `func postItem() async`

**কাজ কী:** নতুন item Firebase-এ upload করা।

**ভিতরে:**

1. `validate()` call
2. `StorageService.uploadImages()` -> image URLs get করা
3. `Item` object create
4. `FirestoreService.createItem()` -> Firestore save
5. success -> `clearForm()`, `didPostSuccessfully = true`
6. failure -> error message show

---

#### G) `func updateItem() async`

**কাজ কী:** existing item update করা।

**ভিতরে:**

1. validate
2. নতুন images থাকলে upload করা
3. removed images থাকলে delete করা
4. item fields update (title/desc/price/category/imageURLs)
5. `updatedAt` timestamp set
6. `FirestoreService.updateItem()` -> save
7. success -> `didEditSuccessfully = true`

---

#### H) `func clearForm()`

**কাজ কী:** form সব field reset করা।

**ভিতরে:** সব @Published state-কে default value দেওয়া।

---

#### I) Computed: `price`, `canAddMoreImages`, `titleCharCount`, `descCharCount`, `totalImageCount`

**কাজ কী:** form field থেকে derived value calculate করা।

**যেমন:**

- `price`: `Double(priceText) ?? 0`
- `canAddMoreImages`: `selectedImages.count < maxImages`
- `charCount`: current + "/" + max দেখানো

---

### 9.27) Mini Data Flow (PostItemViewModel)

1. UI form input -> @Published state change
2. user tap "Post" -> `postItem()` call
3. validation -> image upload -> item create -> success state
4. edit mode-এ: `loadItem()` call -> `updateItem()` flow
5. clear button -> `clearForm()` reset everything

---

### 9.28) Viva/Defense Ready Questions (PostItemViewModel)

1. কেন validation separate method-এ রাখা হয়েছে?
2. edit mode-এ removed image কীভাবে delete হয়?
3. `pickedImage` didSet-এ কেন `nil` set করা হচ্ছে?
4. async/await error handling-এ try/catch structure কি?
5. image URL list update করার সময় কি order matter করে?

---

## 10) Utilities (সংক্ষিপ্ত)

### 10.1) Constants.swift

App-wide constants centralized রাখা। hardcoded value না থাকায় maintain করা সহজ।

#### নিচের constant groups:

- **App Info**: appName, appTagline, universityName
- **Collections**: Firestore collection names (`"users"`, `"items"`)
- **StoragePaths**: Firebase Storage folder paths (`"item_images"`, `"profile_images"`)
- **Departments**: KUET এর 18টি department list
- **Validation rules**:
  - `minPasswordLength = 6`
  - `maxTitleLength = 80`
  - `maxDescriptionLength = 500`
  - `maxPrice = 999999`
  - `maxImages = 3`
- **Colors**: `primary`, `background`, `cardBackground`, `secondaryText`

**কেন দরকার:**

- magic number/string avoid করতে
- একজায়গা থেকে সব সেটিংস change করতে

---

### 10.2) Extensions.swift

String, View, Date, Double এর উপর helper method যোগ করা।

#### A) String Extensions

**`isValidEmail: Bool`**

- regex দিয়ে email format check
- input: self string
- output: `Bool`

**`isValidPhone: Bool`**

- phone 10-14 digit + optional `+` check
- output: `Bool`

**`trimmed: String`**

- whitespace/newline remove করে
- output: trimmed string

---

#### B) View Extensions

**`hideKeyboard()`**

- keyboard dismiss করা
- `UIResponder.resignFirstResponder` action send করে

**`cardStyle() -> some View`**

- reusable card styling (background + corner + shadow)
- input: view
- output: styled view

---

#### C) Date & Double Extensions

**`formattedString: String`** (Date)

- Date কে readable format-এ convert: "Mar 28, 2026, 2:30 PM"

**`formattedAsTaka: String`** (Double)

- number কে Taka symbol সহ format: "৳1500"

---

### 10.3) FirestoreRules.swift

**এটা reference documentation শুধু, code execute হয় না।**

সুপারিশকৃত Firestore & Storage security rules content রাখে।

#### Firestore Rules:

- Users: authenticated only can read, self-create/update
- Items: authenticated can read, self create/update/delete

#### Storage Rules:

- item_images: owner upload/delete (max 5MB)
- profile_images: owner upload/delete (max 2MB)

**কেন দরকার:**

- Firebase Console-এ paste করার reference সঠিক থাকে
- security পরিকল্পনা code-এ documented থাকে

---

### 10.4) NetworkMonitor.swift

Internet connectivity realtime observe করা।

#### A) `static let shared = NetworkMonitor()`

**কাজ:** singleton network monitor instance দেয়।

---

#### B) `@Published var isConnected: Bool`

**কাজ:** internet available কি না track করা।

**Input:** NWPathMonitor update

**Output:** `true`/`false`

---

#### C) `@Published var connectionType: ConnectionType`

**কাজ:** WiFi/Cellular/Wired/Unknown differentiate করা।

**Enum cases:** `.wifi`, `.cellular`, `.wiredEthernet`, `.unknown`

---

#### D) `func startMonitoring()`

**কাজ:** network path monitoring শুরু করা।

**ভিতরে:**

1. `NWPathMonitor` তৈরি করে
2. `pathUpdateHandler` closure set করে
3. path change হলে `isConnected` update হয়
4. `connectionType` ও update হয়

---

#### E) `func stopMonitoring()`

**কাজ:** monitor cancel করা।

**Input/Output:** নেই

---

#### F) `OfflineBannerView`

**কাজ:** `isConnected == false` হলে red banner দেখানো।

**UI:** WiFi icon + "No Internet Connection" text

**কেন দরকার:**

- user দেখতে পারে offline আছে

---

### 10.5) Data Flow (Utilities)

1. Constants → সব service/view hardcoded value replace
2. Extensions → String/View/Date method সর্বত্র ব্যবহার
3. FirestoreRules.swift → developer reference doc
4. NetworkMonitor → MainTabView subscribe করে offline banner trigger করে

---

### 10.6) Viva/Defense Questions (Utilities)

1. কেন constants separate file-এ রাখা হয়েছে?
2. Extension method implement করার সুবিধা vs utility function?
3. NetworkMonitor singleton কেন ব্যবহার করা হয়েছে?
4. FirestoreRules code execute না হওয়া সত্ত্বেও কেন রাখা হয়েছে?
5. `NWPathMonitor` vs অন্যান্য connectivity check method কেন?

---

### 10.7) Progress Update

- [x] KUET_TradeApp.swift
- [x] ContentView.swift
- [x] MainTabView.swift
- [x] AuthViewModel.swift
- [x] AuthService.swift
- [x] FirestoreService.swift
- [x] StorageService.swift
- [x] ItemViewModel.swift
- [x] PostItemViewModel.swift
- [x] Utilities (4 files)
- [ ] পরবর্তী: Models (Item.swift, User.swift)

---

## 11) Views - সংক্ষিপ্ত অপেক্ষা

সব Views UI render করে। ViewModel/Service থেকে data/state নেয় এবং display করে।

---

### 11.1) Auth Views

#### A) LoginView.swift

**কাজ:** email/password দিয়ে login screen render করা।

**Key element:**

- Logo + app name display
- Email/password input fields
- Login button -> `authViewModel.login()` call
- Forgot password link -> ForgotPasswordView sheet
- Sign up link -> NavigationLink to SignUpView
- Loading state: button এ ProgressView

---

#### B) SignUpView.swift

**কাজ:** নতুন account তৈরির form।

**Key fields:**

- Name, Email, Phone, Department picker, Password, Confirm password
- Department dropdown menu (AppConstants.departments থেকে)
- Sign up button -> `authViewModel.signUp()` call
- পরে login page-এ যাওয়ার option

---

#### C) ForgotPasswordView.swift

**কাজ:** password reset email পাঠানো।

**State:**

- `resetEmailSent` false থাকলে email input দেখায়
- true হলে success message দেখায় ("Check Your Email", email address)
- "Back to Login" button দিয়ে dismiss

---

### 11.2) Home Views

#### A) HomeView.swift

**কাজ:** item list browse করার main screen। search + filter UI সহ।

**Key components:**

- Search bar (text input + clear button + filter icon)
- Filter button: badge দিয়ে active filter count দেখায় (নীল chip)
- Active filter tags দেখায় (category/price/sort/search জন্য)
- Item grid (2 column, ScrollView)
- Pull-to-refresh: `itemViewModel.refresh()` call

**ভিতরে:**

- `@ObservedObject var itemViewModel`: item data access
- `showFilterSheet` state: SearchFilterView sheet control করে

---

#### B) ItemCardView.swift

**কাজ:** item list-এ প্রতিটি item-এর small card render করা।

**Display:**

- first image (AsyncImage, loading/failure placeholder সহ)
- Category badge (icon + name) top-right corner-এ
- "SOLD" overlay যদি `!item.isAvailable`
- Title + price + seller name

---

#### C) ItemDetailView.swift

**কাজ:** full item details page। মাল্টিপল images, seller info, contact option সহ।

**Key features:**

- Image gallery (TabView, indicator সহ)
- Sold banner (red) যদি available না
- Item title, description, price
- Seller info card (name, phone, dept, joined date)
- Contact buttons (call/whatsapp/sms) - `ContactSellerButtons` component
- Edit/Delete button (যদি current user = seller)

---

### 11.3) Post Views

#### A) PostItemView.swift

**কাজ:** নতুন item post করার form UI।

**Form sections:**

- Image add section (camera/photo library picker)
- Title input + char count
- Description input + char count
- Price input
- Category selection
- Submit button -> `PostItemViewModel.postItem()` call
- Success view display যখন `didPostSuccessfully = true`

**State management:**

- `@StateObject var viewModel = PostItemViewModel()`: form state
- Sheet/fullScreenCover: image picker UI
- Alert: error message display

---

#### B) EditItemView.swift

**কাজ:** existing item edit করা।

**কীভাবে PostItemView থেকে আলাদা:**

- `loadItem(_ item)` call করে form populate করে
- existing images display করে
- সুযোগ remove করার (swipe action)
- Submit button -> `PostItemViewModel.updateItem()` call

---

### 11.4) Profile Views

#### A) ProfileView.swift

**কাজ:** logged-in user profile page।

**Display:**

- User avatar (initials circle)
- User name, department badge
- Info section: email, phone, dept, joined date
- Share app button (share sheet)
- Sign out button (confirmation বিশ্ব প্রয়োজন)

**Navigation:**

- MainTabView-এ 4th tab

---

#### B) MyAdsView.swift

**কাজ:** user-এর সব posted items manage করা।

**States:**

- Loading view (spinner)
- Empty view (no ads message)
- Item list view (seller-এর items)

**Features:**

- Item count display (toolbar)
- Pull-to-refresh: `loadMyItems()` call
- Swipe actions:
  - Edit -> EditItemView sheet
  - Delete -> confirmation alert
- Mark sold/relist toggle

**Key methods:**

- `loadMyItems()`: `FirestoreService.fetchUserItems(userID:)` call
- `deleteItem()`: Firestore delete + image cleanup

---

### 11.5) Search & Filter

#### A) SearchFilterView.swift

**কাজ:** advanced search/filter sheet (HomeView থেকে open হয়)।

**Sections:**

- Search text input (live filter)
- Category list (All + all ItemCategory)
- Price range inputs (min/max)
- Sort options (newest/oldest/price asc/desc)
- Clear all button

**All input:**

- `@ObservedObject var itemViewModel`: filter state change directly

---

### 11.6) Components

#### A) LaunchScreenView.swift

**কাজ:** app startup এ animated splash screen।

**Animation:**

- logo scale + opacity (0 → 1)
- tagline opacity (0 → 1)
- spinner opacity (0 → 1)
- university name fade in

**Status:** `isCheckingAuth == true` হলে ContentView দ্বারা দেখানো হয়

---

#### B) ContactSellerButton.swift

**কাজ:** call/whatsapp/sms icons + functionality।

**Enum: ContactMethod**

- `.call`, `.whatsApp`, `.sms` (icon, color, label)

**Component: ContactSellerButton**

- Style: `.full` (full-width) বা `.compact` (small icon)
- Tap action: phone number দিয়ে intent trigger
  - Call: `tel://` URL scheme
  - WhatsApp: WhatsApp app সহ URL সহ
  - SMS: `sms://` URL

**Wrapper:**

- `ContactSellerButtons`: full-width call + 2-column whatsapp/sms
- `ContactSellerCompactRow`: 3 icon পাশাপাশি (card use জন্য)

---

#### C) ImagePicker.swift

**কাজ:** UIImagePickerController bridge SwiftUI এ।

**Property:**

- `@Binding var image: UIImage?`
- `sourceType`: `.camera` বা `.photoLibrary`

**কীভাবে:**

- `UIViewControllerRepresentable` protocol implement করে
- `makeUIViewController()`: picker create করে, delegate set করে
- `updateUIViewController()`: নেই
- Delegate method: selected image `@Binding image` set করে

---

#### D) ShimmerView.swift

**কাজ:** skeleton loading placeholder।

**Effect:**

- gray background rectangle
- gradient shimmer animation (left-right slide)
- aspect ratio maintained করে

**Use:** AsyncImage loading হওয়ার সময় temporary visual

---

### 11.7) Data Flow (Views)

1. LoginView/SignUpView -> AuthViewModel -> AuthService -> Firebase
2. HomeView -> ItemViewModel -> FirestoreService -> item list
3. SearchFilterView -> ItemViewModel filter state -> live update
4. PostItemView -> PostItemViewModel -> upload images -> create item
5. ItemDetailView -> contact button -> URL scheme Intent
6. MyAdsView -> user items + edit/delete action
7. ProfileView -> user info display + sign out

---

### 11.8) Viva Questions (Views)

1. HomeView-এ filter state কোথায় রাখা হয়েছে।
2. ItemDetailView কীভাবে detect করে seller নিজে।
3. ImagePicker কেন UIViewControllerRepresentable লাগে।
4. ContactSellerButton different method-দের জন্য কি URL scheme ব্যবহার করে।
5. SearchFilterView কেন separate sheet বনাম inline।
6. LaunchScreenView animation কি state দ্বারা control হয়।

---

### 11.9) Progress Update

- [x] KUET_TradeApp.swift
- [x] ContentView.swift
- [x] MainTabView.swift
- [x] AuthViewModel.swift
- [x] AuthService.swift
- [x] FirestoreService.swift
- [x] StorageService.swift
- [x] ItemViewModel.swift
- [x] PostItemViewModel.swift
- [x] Utilities (4 files)
- [x] Views (14 files)
- [ ] পরবর্তী: Models (Item.swift, User.swift)

---

## 12) All Scenarios & End-to-End Flows

এই section-এ পুরো app-এর major scenario গুলো from কোথা থেকে কোথায় যায়, কে কী করে - একসাথে দেখানো হলো।

---

### 12.1) Master Flow (One Line)

`View (UI input)` -> `ViewModel (state + validation + decision)` -> `Service (Firebase call)` -> `Firebase` -> `ViewModel update` -> `View re-render`

---

### 12.2) App Launch & Routing Flow

1. App start -> `KUET_TradeApp` launch
2. `AppDelegate` -> `FirebaseApp.configure()`
3. `ContentView` load
4. `AuthViewModel.listenToAuthState()` session check করে
5. তিনটা routing outcome:
   - checking চলছে -> `LaunchScreenView`
   - logged in -> `MainTabView`
   - logged out -> `LoginView`

---

### 12.3) Full Auth Flow

#### A) Sign Up Flow

1. `SignUpView` form fill
2. tap Sign Up -> `AuthViewModel.signUp()`
3. `validateSignupFields()` local check
4. `AuthService.signUp(...)` call
5. Service side:
   - Firebase Auth account create
   - profile displayName update
   - Firestore `users/{uid}` doc save
6. success -> `currentUser` set + listener login true
7. UI route -> `MainTabView`

#### B) Login Flow

1. `LoginView` email/password input
2. tap Log In -> `AuthViewModel.login()`
3. validation pass হলে `AuthService.signIn(...)`
4. Firebase session active হয়
5. auth listener callback -> `isLoggedIn = true`
6. `fetchUser()` -> Firestore profile load
7. UI route -> main tabs

#### C) Forgot Password Flow

1. `ForgotPasswordView` email input
2. tap Send -> `AuthViewModel.resetPassword()`
3. Service -> `auth.sendPasswordReset(...)`
4. success -> `resetEmailSent = true`
5. UI success message -> back to login

#### D) Logout Flow

1. `ProfileView` -> Sign Out
2. confirm -> `AuthViewModel.signOut()`
3. Service -> `AuthService.signOut()`
4. listener -> `isLoggedIn = false`, `currentUser = nil`
5. UI route -> `LoginView`

#### E) Auth Error Flow

1. Service throw করে
2. ViewModel `mapAuthError()` দিয়ে human message বানায়
3. `showError = true`
4. View alert দেখায়

---

### 12.4) Full Search/Filter Flow (Home + ViewModel + Service)

#### কে কী করে (Responsibility Split)

- `HomeView`:
  - search bar UI, filter button, filter tags, clear actions
  - user input collect করে
- `SearchFilterView`:
  - advanced filter UI (category/price/sort)
  - একই `itemViewModel`-এ field set করে
- `ItemViewModel`:
  - `allItems` + `filteredItems` maintain করে
  - `applyFilters()`-এ local filtering/sorting করে
  - `didSet` hooks দিয়ে live update করে
- `FirestoreService`:
  - base item data fetch করে (`fetchAllItems`, etc.)
  - এই app-এ final search/filter mostly client-side

#### End-to-End Flow

1. Home open -> `ItemViewModel.loadItems()`
2. Service -> `fetchAllItems()`
3. items আসে -> `allItems` set
4. `applyFilters()` run -> `filteredItems`
5. Home grid shows `filteredItems`
6. user search/category/price/sort change করে
7. `didSet` -> `applyFilters()` auto-run
8. UI instantly refresh হয়

#### কেন HomeView-এও filter, ViewModel-এও filter?

- HomeView: filter **control UI**
- ItemViewModel: filter **business logic**
- Service: filter-এর জন্য **raw data source**

এই separation maintainable architecture দেয়।

---

### 12.5) Post New Item Flow

1. `PostItemView` form fill + image pick
2. submit -> `PostItemViewModel.postItem()`
3. `validate()`
4. `StorageService.uploadImages()` -> image URLs
5. `Item` object build
6. `FirestoreService.createItem(item)`
7. success -> `didPostSuccessfully = true` + form reset
8. Home/MyAds refresh করলে নতুন item visible

#### Post Error Branch

- upload fail / firestore fail -> error message -> alert

---

### 12.6) Edit Item Flow

1. `MyAdsView` থেকে Edit tap
2. `EditItemView` open + `loadItem(existingItem)`
3. user text/image modify করে
4. submit -> `PostItemViewModel.updateItem()`
5. new image থাকলে upload
6. removed old URL থাকলে storage delete চেষ্টা
7. item fields update + `updatedAt`
8. `FirestoreService.updateItem(item)`
9. success -> edit success state + list refresh

---

### 12.7) My Ads Management Flow

1. `MyAdsView.task` -> `loadMyItems()`
2. Service `fetchUserItems(userID:)`
3. UI split: loading / empty / list
4. per item actions:
   - Edit -> `EditItemView`
   - Delete -> confirm -> `deleteItem(byID:)`
   - Sold/Relist -> `toggleAvailability(itemID:isAvailable:)`
5. local list + shared `ItemViewModel` refresh

---

### 12.8) Item Detail & Contact Flow

1. Home card tap -> `ItemDetailView(item)`
2. gallery + details render
3. current user seller কিনা check (`isOwnItem`)
4. buyer হলে contact button visible
5. contact action -> URL scheme open:
   - Call -> `tel://`
   - WhatsApp -> whatsapp URL
   - SMS -> `sms://`

---

### 12.9) Network/Offline Flow

1. `NetworkMonitor.shared.startMonitoring()`
2. path update -> `isConnected` update
3. `MainTabView` observe করে
4. offline হলে `OfflineBannerView` show
5. online ফিরলে banner auto-hide

---

### 12.10) Common State-to-UI Flow

- `isLoading = true` -> button disable / spinner show
- `showError = true` -> alert show
- `didPostSuccessfully = true` -> success screen
- `isRefreshing = true` -> pull-to-refresh indicator
- `hasActiveFilters = true` -> filter chips + badge

---

### 12.11) Scenario Matrix (Quick)

1. **First-time user**: Launch -> Login -> SignUp -> Main tabs -> Post first item
2. **Returning user**: Launch -> auth session restore -> directly Main tabs
3. **Buyer journey**: Home -> Search/filter -> Detail -> Contact seller
4. **Seller journey**: Post -> MyAds -> Edit/Mark sold/Delete
5. **Forgot password**: Login -> Forgot -> Reset email -> back লগইন
6. **Offline user**: Any tab -> offline banner -> limited remote actions

---

### 12.12) Viva/Defense Questions (All Flow)

1. HomeView, ItemViewModel, FirestoreService - search/filter responsibility কিভাবে ভাগ করা?
2. Auth listener-based routing কেন direct manual routing থেকে better?
3. Post flow-এ image আগে upload, তারপর Firestore save - এই order কেন?
4. Edit flow-এ removed images cleanup না করলে কী সমস্যা?
5. MyAds আর Home list consistency কীভাবে maintain হচ্ছে?
6. Offline banner app architecture-এ কোথায় বসানো সবচেয়ে logical এবং কেন?

---

### 12.13) Progress Update

- [x] KUET_TradeApp.swift
- [x] ContentView.swift
- [x] MainTabView.swift
- [x] AuthViewModel.swift
- [x] AuthService.swift
- [x] FirestoreService.swift
- [x] StorageService.swift
- [x] ItemViewModel.swift
- [x] PostItemViewModel.swift
- [x] Utilities (4 files)
- [x] Views (14 files)
- [x] All major scenario + all major flow map
- [ ] পরবর্তী: Models (Item.swift, User.swift)
