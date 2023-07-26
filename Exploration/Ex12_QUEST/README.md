# AIFFEL Campus Online 5th Code Peer Review Templete
- 코더 : 어윤석
- 리뷰어 : 조준규

# PRT(PeerReviewTemplate) 
각 항목을 스스로 확인하고 토의하여 작성한 코드에 적용합니다.

- [X] 코드가 정상적으로 동작하고 주어진 문제를 해결했나요?
  
- [X] 주석을 보고 작성자의 코드가 이해되었나요?
  > 각 코드블록 별로 주석을 자세히 적어주셔서 코드를 쉽게 이해할 수 있었다.
- [X] 코드가 에러를 유발할 가능성이 없나요?
  > 주석과 코드블록을 이용하여 오류가 나타나도 쉽게 수정할 수 있게 하였다. 물론 오류도 일어나지 않았다.
- [X] 코드 작성자가 코드를 제대로 이해하고 작성했나요?
  > 각 코드에서 필요한 개념들을 markdown을 이용하여 많이 정리가 되어있었다.  
  >  코드를 제대로 이해하고 받아들이려는 노력을 특히 볼 수 있었다.
- [X] 코드가 간결한가요?
  > 원하는 바를 수행하기 위해 코드가 군더더기 없이 간결하게 작성되었다.

# 예시
1. 코드의 작동 방식을 주석으로 기록합니다.
2. 코드의 작동 방식에 대한 개선 방법을 주석으로 기록합니다.
3. 참고한 링크 및 ChatGPT 프롬프트 명령어가 있다면 주석으로 남겨주세요.
```python
# 코드 주석 및 간결성 예시
#-----------------------------------------
# 인코더 설계
#-----------------------------------------
encoder_model = Model(inputs=encoder_inputs, outputs=[encoder_outputs, state_h, state_c])

# 이전 시점의 상태들을 저장하는 텐서
decoder_state_input_h = Input(shape=(hidden_size,))
decoder_state_input_c = Input(shape=(hidden_size,))

dec_emb2 = dec_emb_layer(decoder_inputs)

# 문장의 다음 단어를 예측하기 위해서 초기 상태(initial_state)를 이전 시점의 상태로 사용. 이는 뒤의 함수 decode_sequence()에 구현
# 훈련 과정에서와 달리 LSTM의 리턴하는 은닉 상태와 셀 상태인 state_h와 state_c를 버리지 않음.
decoder_outputs2, state_h2, state_c2 = decoder_lstm(dec_emb2, initial_state=[decoder_state_input_h, decoder_state_input_c])

#-----------------------------------------
# 어텐션 메커니즘을 사용하는 출력층 설계
#-----------------------------------------
# 어텐션 함수
decoder_hidden_state_input = Input(shape=(text_max_len, hidden_size))
attn_out_inf = attn_layer([decoder_outputs2, decoder_hidden_state_input])
decoder_inf_concat = Concatenate(axis=-1, name='concat')([decoder_outputs2, attn_out_inf])

# 디코더의 출력층
decoder_outputs2 = decoder_softmax_layer(decoder_inf_concat) 

# 최종 디코더 모델
decoder_model = Model(
    [decoder_inputs] + [decoder_hidden_state_input,decoder_state_input_h, decoder_state_input_c],
    [decoder_outputs2] + [state_h2, state_c2])
```

# 참고 링크 및 코드 개선
```python
# 딥러닝 모델을 이용한 추상적 요약과 Summa를 이용한 추출적 요약을 비교하는 부분이 있으면 좋겠습니다.
# 그래서 어느 방식이 더 효과적인지 비교 분석하여 보여줄 수 있으면 좋겠습니다. 😊

```
