### Project Task List  
Here’s a structured breakdown of tasks to build your spreadsheet DSL tool, organized by priority and complexity.  

---

### 1. RFC & Documentation 
- **Tasks**:  
  - [ ] Draft the RFC document (syntax, semantics, architecture).  
  - [ ] Define formal grammar (BNF/PEG for parser).  
  - [ ] Document error codes and validation rules.  
  - [ ] Create a glossary of terms (e.g., "IR", "virtual variables").  
- **Should the RFC live in the Git repo? 
  - **Yes**. Create an `/rfcs` directory with a `0001-spreadsheet-dsl.md` file.  
  - Use GitHub PRs/issues to track feedback.  

---

### 2. Project Setup 
- **Tasks**:  
  - [ ] Initialize a Rust project with Cargo.  
  - [ ] Set up modular structure:  
    ```  
    /src  
      /compiler      # Parser, AST, IR, exporters  
      /lsp           # Language Server  
      /cli           # Command-line interface  
      /sdk           # Cross-language bindings (FFI/WASM)  
    ```  
  - [ ] Add CI/CD (GitHub Actions for testing/builds).  
  - [ ] Write a `CONTRIBUTING.md` guide.  

---

### 3. Compiler Development 
#### Phase 1: Parser & AST 
- **Tasks**:  
  - [ ] Implement grammar using `pest` or `nom`.  
  - [ ] Define AST structs (e.g., `Table`, `Formula`, `Annotation`).  
  - [ ] Parse annotations (`@compose`, `@style`).  
  - [ ] Handle inheritance (`table A from B`).  

#### Phase 2: Semantic Analyzer 
- [ ] Resolve entity/table references.  
- [ ] Validate formula syntax and types.  
- [ ] Detect circular dependencies.  

#### Phase 3: IR & Exporters 
- [ ] Design IR (platform-agnostic spreadsheet structure).  
- [ ] Implement Excel exporter (`calamine`/`xlsxwriter`).  
- [ ] Add Google Sheets API integration.  

---

### 4. Language Server (LSP) 
- **Tasks**:  
  - [ ] Set up `tower-lsp` boilerplate.  
  - [ ] Implement autocomplete for:  
    - Annotations (e.g., `@compose`).  
    - Entity/column names.  
  - [ ] Add diagnostics (e.g., undefined variables).  
  - [ ] Enable hover tooltips for formulas.  

---

### 5. Dependency Management 
- **Tasks**:  
  - [ ] Design dependency syntax (`@import`).  
  - [ ] Implement a resolver for:  
    - Git-based dependencies (`github:user/repo@v1.0`).  
    - Local files (`./lib/utils.sdsl`).  
  - [ ] Add version locking (`sdsl.lock`).  

---

### 6. Formatter 
- **Tasks**:  
  - [ ] Use `prettyplease` or similar crate for Rust AST formatting.  
  - [ ] Define style rules (indentation, annotation order).  
  - [ ] Add CLI command (`sdsl fmt`).  

---

### 7. Testing & Validation 
- **Tasks**:  
  - [ ] Unit tests for parser/semantic analyzer.  
  - [ ] Integration tests for CLI commands.  
  - [ ] Fuzz testing for edge cases (malformed formulas).  
  - [ ] Benchmark large spreadsheets (>10k rows).  

---

### 8. Cross-Language SDKs 
- **Tasks**:  
  - [ ] Expose Rust core as a C FFI library.  
  - [ ] Build Go SDK using CGO.  
  - [ ] Create JS/TS SDK via WebAssembly (`wasm-pack`).  
  - [ ] Java SDK via JNI.  

---

### 9. Community & Docs 
- **Tasks**:  
  - [ ] Write user guides (basic syntax, CLI usage).  
  - [ ] Create API docs with `rustdoc`.  
  - [ ] Set up GitHub Discussions for Q&A.  
  - [ ] Publish VS Code extension for syntax highlighting.  

---

### 10. Launch Preparation 
- **Tasks**:  
  - [ ] Create a GitHub repo with MIT/Apache 2.0 license.  
  - [ ] Draft a release announcement.  
  - [ ] Prepare a demo video/tutorial.  

---

### Priority Order 
1. **RFC + MVP Compiler**: Focus on parsing, AST, and Excel export.  
2. **LSP**: Enable developer-friendly tooling early.  
3. **Formatter + CLI**: Improve usability.  
4. **Dependency Management**: Unlock collaboration.  

---

### Potential Challenges 
1. **Formula Resolution**: Translating virtual variables (`.up`, `this.row`) to Excel/Sheets cell references.  
   - **Solution**: Build a resolver that tracks cell positions during IR generation.  
2. **Performance**: Large spreadsheets may slow down the LSP.  
   - **Solution**: Incremental parsing + caching.  
3. **Cross-Platform Quirks**: Excel vs. Sheets function names.  
   - **Solution**: Abstract differences in IR-to-exporter logic.  

---

### Next Immediate Steps 
1. Set up the Rust project and Git repo.  
2. Draft the RFC in `/rfcs/0001-spreadsheet-dsl.md`.  
3. Implement the parser (start with `pest` for rapid prototyping).  

Let me know if you want to draft the RFC together or review the parser grammar! 🚀