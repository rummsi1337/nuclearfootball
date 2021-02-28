# nuclearfootball

A kubernetes cluster to go.

## Getting started

- Install requirements via:
    ```
    ansible-galaxy install -r requirements.yaml -p roles
    ```

- Add env var to workaround MacOS fork bug: https://github.com/ansible/ansible/issues/34056#issuecomment-352862252
  ```
  export OBJC_DISABLE_INITIALIZE_FORK_SAFETY=YES
  ```
