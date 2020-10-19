# How to list files from a CLOSED pull request.

GITHUB provides a list of changed files for a Open Pull Request; for a Closed Pull Request it has to extracted manually.
Following code can be helpful

> Run it from browser console 

``` javascript
const fileElems = document.querySelectorAll('#files div.file-info a.link-gray-dark');
const filePaths = [];

for (let a of fileElems) {
    filePaths.push(a.title);
}

const filePathsStr = filePaths.join('\n');
console.log(filePathsStr);
copy(filePathsStr);
console.log('Copied to the clipboard as well 😁');
```
