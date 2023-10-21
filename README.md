# SwiftUI_iOS17_Observation

https://mrprogrammer.medium.com/exploring-the-observation-framework-in-swift-5-9-2a1073bb93a6

https://sarunw.com/posts/observation-framework-in-ios17/

```swift

//
//  SwiftDataFlowApp.swift
//  SwiftDataFlow
//
//  Created by paige shin on 10/21/23.
//

import SwiftUI
import Observation

@Observable 
class User {
    
    var name = ""
    var jobTitle = ""
    var followercount = 0
    @ObservationIgnored
    var bio = ""
    
}

@Observable
class AppState {
    
}

@main
struct SwiftDataFlowApp: App {

    // Don't need anymore @StateObject and @ObservedObject
    @State private var appState = AppState()
    @State private var user = User()

    var body: some Scene {
        WindowGroup {
            ContentView()
                .environment(self.appState)
                .environment(self.user)
        }
    }
}



struct ContentView: View {
   
    @Environment(AppState.self) private var appState
    @Environment(User.self) private var user
    
    
    var body: some View {
        @Bindable var user = self.user
        VStack {
            TextField("", text: $user.name)
        }
        .padding()
    }
}

struct Subview: View {
    
    @Bindable var user: User
    
    var body: some View {
        VStack {
            TextField("", text: self.$user.name)
        }
    }
    
}

struct Subview2: View {
    
    // automatically observed
    var user: User
    
    var body: some View {
        Text(self.user.name)
    }
    
}

#Preview {
    ContentView()
}



```
