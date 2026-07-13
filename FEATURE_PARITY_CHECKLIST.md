# CBrain iOS Feature Parity Checklist

This checklist maps the Android/Desktop whiteboard build to the iOS implementation.

## Main Workbench

- Library open/import: `ContentView`, `LibraryStore`
- Remember/open existing app library: `CBrainViewModel.openExistingLibrary`
- Home node: `CBrainViewModel.homeNode`
- Back/forward history: `CBrainViewModel.openHistory`
- Random note: `CBrainViewModel.openRandomNote`
- Parent/child/related create and existing-link picker: `ContentView`, `CBrainViewModel`
- Rename/delete node: `ContentView`, `CBrainViewModel`
- Parent/sibling/current/child/related graph rows: `ContentView`, `CBrainRepository.siblings`
- Relation removal: `CBrainViewModel.removeRelation`
- Search notes and whiteboard text: `SearchResultsSheet`, `CBrainViewModel.searchWhiteboardTexts`
- Whiteboard search-result jump and focus: `ContentView.openSearchResult`
- Whiteboard status/info for current node: `CBrainViewModel.updateWhiteboardStatus`
- Markdown note save/edit/preview/maximize: `ContentView`
- Markdown bold/highlight wrappers: `ContentView`
- Copy selected note text as CBrain reference link: `ContentView.copyReferenceLink`
- S3 sync/check/download-all: `S3SettingsView`, `CBrainViewModel`, `CBrainSyncService`

## Whiteboard Storage

- Android-compatible `drawings.json`: `WhiteboardRepository`
- Android-compatible `canvas/<drawingId>.json`: `WhiteboardRepository`
- Existing array/object drawings index formats: `WhiteboardRepository.loadIndex`
- Create/open/delete drawing: `WhiteboardRepository`
- Canvas modified time and save: `WhiteboardRepository`
- Whiteboard usage info by node: `WhiteboardRepository.usageInfo`

## Whiteboard Canvas

- Text, rectangle, circle, arrow, line tools: `WhiteboardView`, `WhiteboardDocument`
- Undo/redo: `WhiteboardDocument`
- Delete selected element: `WhiteboardDocument.deleteSelection`
- Copy/paste selected elements through pasteboard: `WhiteboardDocument.copySelection`, `paste`
- Group/ungroup selected elements: `WhiteboardDocument.groupSelection`, `ungroupSelection`
- Text color choices: `WhiteboardDocument.changeSelectedTextColor`
- Node card insertion from search: `WhiteboardDocument.addNoteNode`
- Canvas text search/focus: `WhiteboardSearchView`, `WhiteboardDocument.focusElement`
- Marquee selection: `WhiteboardCanvasUIView`
- Drag selection: `WhiteboardDocument.moveSelection`
- Resize selected element: `WhiteboardDocument.resizeElement`
- Connector endpoint drag: `WhiteboardCanvasUIView`
- Connector endpoint snap/binding: `WhiteboardDocument.snapConnectorEndpoint`
- Connector label edit and positioning: `WhiteboardDocument.commitConnectorLabel`
- Shape-centered text edit: `WhiteboardDocument.centeredTextElement`
- Bound connector updates before save: `WhiteboardDocument.normalizeElementsBeforeSave`
- Full canvas-only mode: `WhiteboardView.canvasOnly`
- Bottom graph/note panel in whiteboard: `WhiteboardView`

## Known Platform Difference

- Android can request broad filesystem access and download S3 into a user-selected external folder. iOS is sandboxed; the iOS download-all action writes into the app library folder managed by `LibraryStore`.
- Local Windows cannot run `xcodebuild`; use the included GitHub Actions macOS workflow to compile.
