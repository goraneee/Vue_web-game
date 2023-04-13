<template>
  <div>
    <h1>{{ result }}</h1>
    <form @submit.prevent="onSubmitForm">
      <input ref="answer" minlength="4" maxlength="4" v-model="value" />
      <button>입력</button>
    </form>
    <div>시도: {{ tries.length }}</div>
    <ul>
      <li v-for="t in tries" :key="t.try">
        <div>
          {{ t.try }}: {{ t.result }}
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
    const getNumbers = () => {
        const candidates = [1, 2, 3, 4, 5, 6, 7, 8, 9];
        const array = [];
        for (let i = 0; i < 4; i += 1) {
            const chosen = candidates.splice(Math.floor(Math.random() * (9 - i)), 1)[0];
            array.push(chosen);
        }
    return array;
    };

export default {
  data() {
    return {
      answer: getNumbers(), // 정답은 배열 형태 ex. [1, 5, 3, 4]
      tries: [],
      value: '',
      result: '',
    }
  },
  methods: {
    onSubmitForm() {
        
        // 맞춘 경우
        if(this.value === this.answer.join('')){    // 문자열과 배열은 join()해줘야 비교 가능
            this.tries.push({
                try: this.value,
                result: `홈런`,
            });

            this.result = `홈런`;
            alert('게임을 다시 실행합니다.');
            this.value = '';    // 초기화
            this.tries = [];
            this.$refs.answer.focus();
        }else{  // 틀린 경우

            if(this.tries.length >= 9){
                this.result = `10번 넘게 틀려서 실패! 답은 ${this.answer.join(',')} 였습니다.`;
                alert("게임을 다시 시작합니다. ");
                this.value = '';    // 초기화
                this.answer = getNumbers();    
                this.tries = [];
                this.$refs.answer.focus();
            }

            let strike = 0;
            let ball = 0;
            const answerArr = this.value.split('').map(v => parseInt(v));

            for(let i = 0; i < 4; i += 1){
                if(answerArr[i] === this.answer[i] ){   // 숫자와 자릿수 모두 맞는 경우: 스트라이크
                    ++strike;
                }else if(this.answer.includes(answerArr[i])){ // 볼
                    ++ball;
                }
            }

            this.tries.push({
                try: this.value,
                result : `${strike} 스트라이크, ${ball} 볼입니다.`
            });

            this.value = '';
            this.$refs.answer.focus();
        }
    }
  }
};
</script>

<style></style>
