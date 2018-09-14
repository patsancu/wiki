# [How to add an image to a gist](https://remarkablemark.org/blog/2016/06/16/how-to-add-image-to-gist/)

1. Create or find a [gist](https://gist.github.com) that you own.
2. Clone your gist (replace `<hash>` with your gist's hash):
    ```sh
    # with ssh
    git clone git@gist.github.com:<hash>.git mygist

    # with https
    git clone https://gist.github.com/<hash>.git mygist
    ```

3. Change to your gist’s directory:
   ```sh
   cd mygist
   ```

4. Add and commit the image:
    ```sh
    git add tulip.jpg
    git commit -m "Add tulip to gist"
    ```

5. Update remote:
    ```sh
    git push origin master
    ```

See blog [post](https://remarkablemark.org/blog/2016/06/16/how-to-add-image-to-gist/).
