It looks like you're facing issues pushing your local Git repository to GitHub due to large files that exceed GitHub's file size limit. To resolve this issue, you have a few options:

1. **Git LFS (Large File Storage):** Since you mentioned that you tried Git LFS but faced issues, you can try reconfiguring Git LFS and pushing your files again.

   First, make sure you have Git LFS installed globally:
   
   ```
   git lfs install
   ```

   Then, configure Git LFS for your repository:

   ```
   git lfs track "pretrained_models/mol2vec/model_300dim.pkl"
   git lfs track "raw_data/stitch/chemical_chemical.links.v5.0.tsv/chemical_chemical.links.v5.0.tsv"
   git lfs track "raw_data/drugbank/drugbank_all_full_database.xml/full_database.xml"
   ```

   Once tracking is set up, commit the changes:

   ```
   git add .gitattributes
   git commit -m "Configure Git LFS for large files"
   ```

   Finally, try pushing your changes again:

   ```
   git push
   ```

2. **Remove Large Files:** If you want to push your repository without using Git LFS, you can remove the large files from your Git history. This will make your repository smaller and within GitHub's limits. However, this will rewrite the Git history, so use caution if others are collaborating on the repository.

   To remove large files from Git history, you can use the `filter-branch` command. Replace `large_file_name` with the actual file names:

   ```
   git filter-branch --force --index-filter 'git rm --cached --ignore-unmatch large_file_name' --prune-empty --tag-name-filter cat -- --all
   ```

   Then, force-push your changes:

   ```
   git push -f
   ```

   After this, your repository should be smaller, and you can push it to GitHub without exceeding file size limits.

3. **GitHub Releases:** If the large files are necessary but not for the main repository, consider using GitHub Releases. You can upload large files as releases rather than pushing them to the main repository. This keeps your main repository smaller.

4. **Split Large Files:** If the large files are not crucial for the entire repository, consider splitting them into smaller chunks or finding alternative ways to host them (e.g., external storage or download links) and then update your code accordingly.

Remember that rewriting Git history can be risky, especially if others are collaborating on the repository. It's essential to communicate with your team if you choose this approach.