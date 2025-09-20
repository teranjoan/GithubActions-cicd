# Passing Values Between Jobs Demo Action

This composite action demonstrates various techniques for passing and using variables in GitHub Actions:

## 🎯 What it demonstrates

- **Variable Generation**: Creating dynamic variables with timestamps and random numbers
- **Step Outputs**: Using `${{ steps.id.outputs.variable }}` to pass data between steps
- **Complex Data**: Creating and parsing JSON data structures
- **Action Outputs**: Exposing data for use in calling workflows

## 📋 Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `demo_prefix` | Prefix for the generated app name | No | `MyApp` |

## 📤 Outputs

| Output | Description | Example |
|--------|-------------|---------|
| `generated_name` | The generated app name | `ActionDemo-20250920` |
| `build_time` | When the build was created | `2025-09-20 14:30:15` |
| `build_number` | Random build number generated | `742` |
| `app_info_json` | Complex JSON data structure | `{"name":"...","buildTime":"..."}` |

## 🚀 Usage

### Basic usage:
```yaml
steps:
  - name: Run demo action
    id: demo
    uses: teranjoan/GithubActions-cicd/.github/actions/passing_values_between_jobs@master
    with:
      demo_prefix: "MyProject"
  
  - name: Use the outputs
    run: |
      echo "App name: ${{ steps.demo.outputs.generated_name }}"
      echo "Build time: ${{ steps.demo.outputs.build_time }}"
      echo "Build number: ${{ steps.demo.outputs.build_number }}"
```

### Using JSON output:
```yaml
steps:
  - name: Run demo action
    id: demo
    uses: teranjoan/GithubActions-cicd/.github/actions/passing_values_between_jobs@master
  
  - name: Parse JSON output
    run: |
      echo '${{ steps.demo.outputs.app_info_json }}' | jq '.'
      APP_NAME=$(echo '${{ steps.demo.outputs.app_info_json }}' | jq -r '.name')
      echo "Extracted app name: $APP_NAME"
```

## 🔍 What you'll learn

1. **Step-to-step communication**: How to pass variables between steps using `$GITHUB_OUTPUT`
2. **Output exposure**: How to make internal variables available to calling workflows
3. **JSON handling**: Creating and parsing complex data structures
4. **Conditional logic**: Using generated values in conditional statements

## 💡 Key concepts demonstrated

- `$GITHUB_OUTPUT` for setting step outputs
- `${{ steps.id.outputs.variable }}` for reading step outputs
- JSON creation with heredoc syntax
- JSON parsing with `jq`
- Action output definition in `action.yml`

This action serves as a practical example for understanding data flow in GitHub Actions workflows.