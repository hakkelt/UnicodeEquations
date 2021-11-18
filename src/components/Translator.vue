<template>
    <textarea id="equation-input" v-model="equation" placeholder="Type your equation here" name="equation" />
    <pre id="output">{{translated}}</pre>
</template>

<style scoped>
    #equation-input {
        width: 80%;
        max-width: 800px;
        border-color: black;
        border-radius: 3px;
    }
    #output {
        border-style: solid;
        border-color: black;
        border-radius: 3px;
        border-width: 1px;
        width: calc(80% - 6px);
        max-width: 800px;
        margin: auto;
        margin-top: 5px;
        padding: 5px;
        text-align: left;
        font-family: Verdana, Geneva, Tahoma, sans-serif;
        font-size: 80%;
    }
</style>

<script>
import data from './codeTable';
export default {
  data() {
    return {
      equation: '\\scrT(x) = \\phi \\div x\\^2, \\phi \\in \\bbR'
    }
  },
  computed: {
    translated() {
        const re = /\\[^\\ ]+/g;
        if (this.equation.trim() == '')
            return "your unicode equation will appear here";
        let translatedEquation = this.equation;
        const matches = [...this.equation.matchAll(re)];
        for (const match of matches) {
            for (let len = match[0].length; len > 2; len--) {
                const searched = match[0].substr(0, len);
                const substitution = checkForSubstitution(searched)
                if (substitution !== null)
                    translatedEquation = translatedEquation.replace(searched, substitution);
            }
        }
        return translatedEquation;
    }
  }
}

function checkForSubstitution(searched) {
    for (const record of data) {
        if (typeof record.completion === 'string' && record.completion == searched) {
                return record.char;
        } else if (typeof record.completion === 'object') {
            for (const comp of record.completion) {
                if (comp == searched) {
                    return record.char;
                }
            }
        }
    }
    return null;
}
</script>
