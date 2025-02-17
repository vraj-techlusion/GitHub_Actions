# GitHub Context in GitHub Actions

In GitHub Actions, context is a way to access and use metadata related to a workflow run, such as event details, repository information, actor details, and job parameters.

GitHub provides predefined contexts that can be used inside workflows to dynamically reference information.

## Types of GitHub Contexts

GitHub contexts are available using `${{ }}` syntax inside workflow files.

### 1. `github` Context

Provides metadata about the GitHub repository, workflow, event, and actor.

**Example:**

```yaml
steps:
    - name: Print GitHub context
        run: echo "Repository: ${{ github.repository }} | Actor: ${{ github.actor }}"
```

**Common properties:**

| Property           | Description                               | Example                  |
|--------------------|-------------------------------------------|--------------------------|
| `github.repository`| Full repo name                            | `vrajclerk/my-repo`      |
| `github.actor`     | Username who triggered the workflow       | `vrajclerk`              |
| `github.event_name`| Event type triggering the workflow        | `push`, `pull_request`   |
| `github.ref`       | Git ref of the branch or tag              | `refs/heads/main`        |
| `github.sha`       | Commit SHA that triggered the workflow    | `f45d6b3...`             |

### 2. `job` Context

Provides information about the current job.

**Example:**

```yaml
steps:
    - name: Print Job Status
        run: echo "Job Status: ${{ job.status }}"
```

**Common properties:**

| Property    | Description                          |
|-------------|--------------------------------------|
| `job.status`| Status of the current job (success, failure, cancelled) |

### 3. `steps` Context

Access outputs from previous steps in the job.

**Example:**

```yaml
steps:
    - name: Generate a value
        id: step1
        run: echo "MY_VAR=Hello" >> $GITHUB_ENV

    - name: Use step output
        run: echo "Value is ${{ steps.step1.outputs.MY_VAR }}"
```

**Common properties:**

| Property                          | Description               |
|-----------------------------------|---------------------------|
| `steps.<step_id>.outputs.<name>`  | Get output from a step    |

### 4. `runner` Context

Provides information about the runner executing the job.

**Example:**

```yaml
steps:
    - name: Print Runner Info
        run: echo "Running on: ${{ runner.os }}"
```

**Common properties:**

| Property     | Description           | Example         |
|--------------|-----------------------|-----------------|
| `runner.os`  | OS of the runner      | `Linux`, `Windows`, `macOS` |
| `runner.arch`| Architecture          | `X64`, `ARM64`  |

### 5. `secrets` Context

Used to access GitHub secrets securely.

**Example:**

```yaml
steps:
    - name: Use Secret
        run: echo "Token: ${{ secrets.MY_SECRET }}"
```

Secrets are masked in logs.

### 6. `env` Context

Access environment variables.

**Example:**

```yaml
steps:
    - name: Set Env Var
        run: echo "MY_VAR=Hello" >> $GITHUB_ENV

    - name: Use Env Var
        run: echo "Value: ${{ env.MY_VAR }}"
```

**Common properties:**

| Property       | Description                  |
|----------------|------------------------------|
| `env.<var_name>`| Gets an environment variable |