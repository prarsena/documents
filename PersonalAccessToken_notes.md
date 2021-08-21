There is no more password-based authentication in GitHub. 
When you try to push to a remote branch, you are greeted with this message: 

      user@host repo % git push -u origin main
      remote: Support for password authentication was removed on August 13, 2021. Please use a personal access token instead.
      remote: Please see https://github.blog/2020-12-15-token-authentication-requirements-for-git-operations/ for more information.
      fatal: unable to access 'https://github.com/username/repo.git/': The requested URL returned error: 403

In order to use a PAT in practice:   
1. Generate a Personal Access Token (described in article above). 
2. If you already added a remote repo, remove it: `git remote rm origin`
3. Add the remote repo again, including your credentials before the repo URL:
      `remote add origin https://<your_username>:<your_token>@github.com/username/repo.git`
4. Push your changes: `git push origin main`


PATs are also needed for cloning private repos. Can be done using the same format described in step 3. 
`git clone https://<your_username>:<your_token>@github.com/username/repo.git`
