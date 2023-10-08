### E2 - GitHub Actions: Build CI pipelines
1. How was integration done in the past?
2. What probles does CI solve?
3. How does cPython do CI?
4. Demo
   
1> Automate the Build

2> Introduce Automated test : Unit Tests, Integration, ...

3> Linking(Unified Code Style)

4> Security/Scaring

name: Tests

on:
  workflow_dispatch:
  push:
    branches:
    - 'main'
    - '3.10'
    - '3.9'
    - '3.8'
    - '3.7'

  pull_request:
    branches:
    - 'main'
    - '3.10'
    - '3.9'
    - '3.8'
    - '3.7'
    
