<template>
      <div class="start__page js__start__page">
        <p class="desc">Осталось пройти небольшой тест,  который покажет, как хорошо ты усвоил материал</p>
        <div class="points__cont">
            <ul class="points__list">
                <li class="point">
                   <span>&ndash;</span>Для успешного прохождения нужно правильно ответить минимум на 7 вопросов из 10
                </li>
                <li class="point">
                    <span>&ndash;</span>На прохождение теста дается 3 попытки
                </li>
            </ul>
        </div>
        <div class="start__btn__cont">
            <button class="start js__start" @click="() => { start(); load_test(); }">
            Начать
            <img src="../../public/items/next.png" alt="">
        </button>
        </div>
      </div>
  </template>
  <script>
      export default {
        props: ['start', 'load_test'],
          data(){
              return {
       
		    }
        },
		mounted(){
		
		},

		methods: {
			
				}
					
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

@mixin flex__params($horiz, $vert, $dir){
    display: flex;
    flex-direction: $dir;
    align-items: $horiz;
    justify-content: $vert;
}

        .start__page{
            min-height: 468px;
            height : auto;
              .desc{
                    font-size: 18px;
                    margin-left: 30px;
                }
                .points__cont{
                    width: 940px;
                    height: 86px;
                    padding: 15px;
                    margin: 30px;
                    border-radius: 10px;
                    background-color: #FFEFE0;
                    @include flex__params(start, center, column);
                    .points__list{
                        @include flex__params(start, start, column);
                        gap: 1rem;
                        list-style: none;
                        .point{
                            font-size: 16px;
                            span{
                                margin: 0 10px 10px 0;
                                color: red;
                                font-weight: 600;
                            }
                        }
                    }
                }
                .start__btn__cont{
                    width: 100%;

                    @include flex__params(center, center, column);
                    .start{
                    width: 940px;
                    height: 61px;
                    background-color: red;
                    color: white;
                    border: none;
                    font-size: 18px;
                    font-weight: 700;
                    border-radius: 15px 15px 0 0;
                    @include flex__params(center, center, row);
                    img{
                        margin-left: 20px;
                    }
                }
            }
        }
</style>