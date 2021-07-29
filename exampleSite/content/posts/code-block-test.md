---
title: Code Block Test
date: 2021-06-27 09:00:00
tags:
    - test
categories:
    - tech
keywords:
    - markdown
    - code block
---


`String`

Using indents:

    text
    text
    text


Fenced code block:

```
text
text
<tag>
```

Fenced code block with language (lineNumbersInTable = false):

```Java
// JavaJavaJavaJavaJavaJavaJavaJavaJavaJavaJavaJavaJavaJavaJavaJavaJavaJavaJavaJavaJavaJavaJavaJavaJavaJavaJavaJavaJavaJava
public final class String
    implements java.io.Serializable, Comparable<String>, CharSequence
{
    /** The value is used for character storage. */
    private final char value[];

    /** The offset is the first index of the storage that is used. */
    private final int offset;

    /** The count is the number of characters in the String. */
    private final int count;

    /** Cache the hash code for the string */
    private int hash; // Default to 0

    // ...

    // Package private constructor which shares value array for speed.
    String(int offset, int count, char value[]) {
        this.value = value;
        this.offset = offset;
        this.count = count;
    }

    // ...

    /**
     * Returns a new string that is a substring of this string. The
     * substring begins at the specified <code>beginIndex</code> and
     * extends to the character at index <code>endIndex - 1</code>.
     * Thus the length of the substring is <code>endIndex-beginIndex</code>.
     * <p>
     * Examples:
     * <blockquote><pre>
     * "hamburger".substring(4, 8) returns "urge"
     * "smiles".substring(1, 5) returns "mile"
     * </pre></blockquote>
     *
     * @param      beginIndex   the beginning index, inclusive.
     * @param      endIndex     the ending index, exclusive.
     * @return     the specified substring.
     * @exception  IndexOutOfBoundsException  if the
     *             <code>beginIndex</code> is negative, or
     *             <code>endIndex</code> is larger than the length of
     *             this <code>String</code> object, or
     *             <code>beginIndex</code> is larger than
     *             <code>endIndex</code>.
     */
    public String substring(int beginIndex, int endIndex) {
        if (beginIndex < 0) {
            throw new StringIndexOutOfBoundsException(beginIndex);
        }
        if (endIndex > count) {
            throw new StringIndexOutOfBoundsException(endIndex);
        }
        if (beginIndex > endIndex) {
            throw new StringIndexOutOfBoundsException(endIndex - beginIndex);
        }
        return ((beginIndex == 0) && (endIndex == count)) ? this :
            new String(offset + beginIndex, endIndex - beginIndex, value);
    }

    // ...
}
```

Using hugo's `highlight` [shortcode]([highlight](https://gohugo.io/content-management/syntax-highlighting/#highlight-shortcode)) (lineNumbersInTable = true):

{{< highlight typescript "linenos=table, hl_lines=8 18-21" >}}
// TypeScript
type OptionalUser = {
    [K in keyof User]?: User[K]
}

// ! we can remove optional constraint
type RequiredUser = {
    [K in keyof OptionalUser]-?: User[K]
}

type NullableUser = {
    [K in keyof User]: User[K] | null
}
type ReadonlyUser = {
    readonly [K in keyof User]: User[K]
}

// ! we can remove readonly constraint
type ModifiableUser = {
    -readonly [K in keyof User]: User[K]
}
{{< /highlight >}}

Without line number

{{< highlight javascript "linenos=false" >}}
(() => {

  function createCopyButton(codeNode) {
    const copyBtn = document.createElement('button')
    copyBtn.className = 'code-copy-btn'
    copyBtn.type = 'button'
    copyBtn.innerText = 'copy'
    copyBtn.parentElement = codeNode.parentElement

    let resetTimer
    copyBtn.addEventListener('click', () => {
      navigator.clipboard.writeText(codeNode.innerText).then(() => {
        copyBtn.innerText = 'copied!'
      }).then(() => {
        clearTimeout(resetTimer)
        resetTimer = setTimeout(() => {
          copyBtn.innerText = 'copy'
        }, 1000)
      })
    })

    return copyBtn
  }

  document.querySelectorAll('pre > code').forEach((codeNode) => {
    const copyBtn = createCopyButton(codeNode);
    codeNode.parentNode.insertBefore(copyBtn, codeNode)
  })

})()
{{< / highlight >}}
