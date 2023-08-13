<template>
  <h1>11. Write a function which count the number of occurrence of a word in a paragraph or a sentence.The function countWords takes a paragraph and word as parameters.</h1>
  <div class="example">
    <code>const paragraph = 'I love teaching. If you do not love teaching what else can you love. I love JavaScript if you do not love something which can give life to your application what else can you love.';
      <pre>console.log(countWords(paragraph,'love', 'you'));
The word love more frequently occurred than you.</pre></code>
  </div>
  <p>{{ whichMoreOccure(countWords(text, 'love', 'you', 'not')) }}</p>
</template>

<script setup lang="ts">
const text = 'I love teaching. If you do not love teaching what else can you love. I love JavaScript if you do not love something which can give life to your application what else can you love.'

function countWords(...args: string[]): [string,number][] {
  const [paragraph, ...words] = args
  return words.map(w => [w, (paragraph.match(RegExp(w,'g')) || []).length] )
}

function whichMoreOccure(args: [string, number][]) {
  let max: [string, number] = ['', 0]
  args.forEach((a: [string, number]) => {
    if(a[1] &&  a[1] > max[1]) max = a
  })
  return `The word "${max[0]}" more frequently occurred (${max[1]}) than: ${getListWithNumber(args.filter(e => e !== max))}`
}

function getListWithNumber(list: [string, number][]) {
  return list.map(e => ` "${e[0]}" -> ${e[1]}`)
}
</script>