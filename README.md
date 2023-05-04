# Onboarding-Afroz
| <img src="https://github.com/Brian-McIntosh/Onboarding-Afroz/blob/main/images-Afroz/1.png" width="250"/>        | <img src="https://github.com/Brian-McIntosh/Onboarding-Afroz/blob/main/images-Afroz/2.png" width="250"/>           |
| ------------- |:-------------:|

```swift
struct ContentView: View {
    
    @AppStorage("shouldShowOnboarding") var shouldShowOnboarding = true
    
    var body: some View {
        NavigationStack {
            VStack {
                Image(systemName: "homekit")
                    .resizable()
                    .scaledToFit()
                    .frame(width: 80, height: 80)
                    .foregroundColor(.accentColor)
                Text("You are in the main app now!")
                    .font(.title)
                Text(".fullScreenCover(isPresented: $shouldShowOnboarding")
            }
            .padding()
            .navigationTitle("Home")
        }
        .fullScreenCover(isPresented: $shouldShowOnboarding) {
            OnboardingView(shouldShowOnboarding: $shouldShowOnboarding)
        }
    }
}

// How do we show a view modally?
// Create another view and bind it to a @State var.
// Logan - CONTAINER VIEW
struct OnboardingView: View {
    
    @Binding var shouldShowOnboarding: Bool
    
    var body: some View {
        TabView { // Horizontal scrolling!
            PageView(
                title: "Push Notifications",
                subtitle: "Enable notifications to stay up to date",
                imageName: "bell",
                showsDismiss: false,
                shouldShowOnboarding: $shouldShowOnboarding
            )
            PageView(title: "Bookmarks",
                     subtitle: "Save your favorites",
                     imageName: "bookmark",
                     showsDismiss: false,
                     shouldShowOnboarding: $shouldShowOnboarding
            )
            PageView(title: "Flights",
                     subtitle: "Book flights to the places",
                     imageName: "airplane",
                     showsDismiss: false,
                     shouldShowOnboarding: $shouldShowOnboarding
            )
            PageView(title: "Home",
                     subtitle: "Go home wherever you might be",
                     imageName: "house",
                     showsDismiss: true,
                     shouldShowOnboarding: $shouldShowOnboarding
            )
        }
        .tabViewStyle(.page)
    }
}

// REPEATABLE VIEW
struct PageView: View {
    let title: String
    let subtitle: String
    let imageName: String
    let showsDismiss: Bool
    @Binding var shouldShowOnboarding: Bool
    var body: some View {
        VStack {
            Image(systemName: imageName)
                .resizable()
                .scaledToFit()
                .frame(width: 150, height: 150)
                .padding()
            Text(title)
                .font(.system(size: 32))
                .padding()
            Text(subtitle)
                .font(.system(size: 24))
                .multilineTextAlignment(.center)
                .padding()
            if showsDismiss {
                Button {
                    shouldShowOnboarding.toggle()
                } label: {
                    Text("Get Started")
                        .bold()
                        .foregroundColor(Color.white)
                        .frame(width: 200, height: 50)
                        .background(Color.green)
                        .cornerRadius(6)
                }
            }
        }
    }
}
```
