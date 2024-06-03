<template>
	<div class="outer__cont">
		<Header></Header>
		<h1>Тестирование</h1>
		<main>
			<StartPage 
			v-if="!isStarting" 
			v-bind:start="Start"
			v-bind:load_test="GetData"/>

				<div class="quiz__cont" v-else>
					<form v-for="qa in QA__array">
						<p v-if="qa.isShowing">{{ qa.question }}</p>
						<div v-for="ans in qa.answers">
							<label v-if="qa.isShowing" v-bind:for="ans">
								<input v-if="qa.isShowing"
								type="radio"
								v-bind:id="ans"
								v-bind:value="ans"
								v-model="last__answer"
								name="answer">
								{{ ans }}
						</label>
						</div>
					</form>
					<button v-if="isStarting && !test__complete" @click="ShowNext">Принять</button>
					<button v-if="test__complete" @click="CheckAnswers(this.user__answers)">Принять</button>
				</div>
		</main>
		<Footer></Footer>
	</div>



</template>
<script>
	import Header from './components/Header.vue'
	import Footer from './components/Footer.vue';
	import StartPage from './components/StartPage.vue';
	
	export default {
		components: {
			Header,
			Footer,
			StartPage

		},
          data(){
              return {
				isStarting: false,
				QA__array: "",
				last__answer: "",
				user__answers: [],
				test__complete: false
		    }
		},
		mounted(){
		
		},

		methods: {
		
			Start(){
				console.log("start");
				this.isStarting = true;
			},
			async GetData(){
				const data = await fetch('src/components/qArray.json');
				this.QA__array =  await data.json();
				console.log(this.QA__array)
    		},
			CheckAnswers(arr){
				let res__counter = 0;
				for(let i = 0; i < arr.length; i++)
				{
					if(arr[i] == this.QA__array[i].correct_answer){
						res__counter++;
					}
				}
				console.log(res__counter)
			},
			ShowNext(){
				this.user__answers.push(this.last__answer)
				for(let i = 0; i < this.QA__array.length; i++)
				{
					const showing__q = this.QA__array;
					if(showing__q[i].isShowing == true)
					{
						showing__q[i].isShowing = false;
						if(i < showing__q.length - 1){
							showing__q[i + 1].isShowing = true;
						}
						else{
							this.test__complete = true;
							console.log(this.user__answers)
							return
						}
						return
					}	
				}	
		
			},
			
		},

	}

</script>
<style scoped lang="scss">
		*{
    padding: 0;
    margin: 0;
    box-sizing: border-box;
    font-family: Arial, Helvetica, sans-serif;
    font-size: 14px;
}  

.outer__cont{
    width: 1000px;
	height: auto;
		h1{
			margin: 75px 0px 30px 30px;
			font-size: 38px; 
		}
		main{
			width: 100%;
			min-height: 468px;
			height: auto;
			.quiz__cont{
				width: 1000px;
				height: auto;

			// .quiz{

				// }

				

			}
		}
	

}





</style>
