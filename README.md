# Swift-UI-sheets-lesson
Swift UI sheets lesson
![sheets](https://github.com/danielurra/Swift-UI-sheets-lesson/assets/51704179/a369f4e0-5cec-4619-8c6e-636e6f67c368)<br>
## Grab the code - Create Journal Entry file
```swift
//
//  CreateJournalEntryView.swift
//  JournalEntries
//
//  Created by Eusebio Taba on 3/27/24.
//

import SwiftUI

struct CreateJournalEntryView: View {
    var body: some View {
        Text("CREATE JOURNAL ENTRY")
    }
}

#Preview {
    CreateJournalEntryView()
}
```
## Grab the code - Journal Entry List View file
```swift
//
//  ContentView.swift
//  JournalEntries
//
//  Created by Eusebio Taba on 3/20/24.
//

import SwiftUI
import SwiftData

struct JournalEntriesListView: View {
    @Environment(\.modelContext) private var modelContext
    @Query private var arrayPlural: [jedi]
    
    @State var showCreateView = false
    
    var body: some View {
        NavigationStack {
            List (arrayPlural){ iterateArrayMembers in
                NavigationLink(destination: JournalEntryDDetailView(detailJournalEntry: iterateArrayMembers)){
                    RowDetailView(rowJournalEntry: iterateArrayMembers)
                }
            }
            .navigationTitle("\(arrayPlural.count) Journal Entries")
            .toolbar {
                Button(action: {
//                    let newJedi = jedi(title: "Hello Amiguito", depunoyletra: "I'm learning SwiftData", rating: 7, timestamp: Date())
//                    modelContext.insert(newJedi)
                    showCreateView = true
                }) {
                    Label("Add Item", systemImage: "plus")
                }
            }
            .sheet(isPresented: $showCreateView){
//                aqui va la nueva view
                CreateJournalEntryView()
            }
        }
    }
}

#Preview {
    JournalEntriesListView()
        .modelContainer(for: jedi.self, inMemory: true)
}
```
