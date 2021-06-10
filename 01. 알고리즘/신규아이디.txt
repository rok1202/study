def check_word(new_id):
    answer = []
    length = len(new_id)-1
    idx = 0
    cnt = 0

    while length >= 0 :
        if new_id[idx].isalpha() :
            answer.append(new_id[idx])		# 현재 index의 문자가 영문이면 Answer에 포함.

        if new_id[idx].isdigit() :			# 현재 index의 문자가 숫자면 Answer에 포함.
            answer.append(new_id[idx])   
         
        if new_id[idx] == '_' or new_id[idx] == '-':
            answer.append(new_id[idx])   	# 현재 index의 문자가 '-'이거나 '_'이면 Answer에 포함.

        if new_id[idx] == '.' :
            if idx ==len(new_id)-1 or idx == 0 or new_id[idx-1] == '.':		# 문자열 양끝에 dot(.)이 오거나 연속된 dot이 올 경우 이를 무시.
                pass
            else : 
                answer.append(new_id[idx])				# 그게 아니면 Answer에 포함.
        if new_id[idx] == ' ' :
            new_id[idx] =='a'						# 만약 빈 문자열이면 이를 'a'로 치환.
        else :
            pass
        
        idx += 1
        length -= 1
        
    answer = "".join(answer)			# join을 통해 문자열로 만들어줌.			
    return answer


def solution(new_id):
    answer = []
    real_ans = []
    new_id = list(new_id.lower())		# 문자열 내에 포함된 모든 알파벳을 소문자로 변경.
    answer = check_word(new_id)		# Check
    answer = check_word(answer)		# 문자열 내에 포함된 모든 알파벳을 소문자로 변경.
    for i in range(0, len(new_id)-1):		# 문자열 내에 포함된 모든 알파벳을 소문자로 변경.
        answer = check_word(answer)

    answer = list(answer)
    length = len(answer)
    if length >= 15 :			# 검토된 문자열 길이15자가 넘어가면 15자까지만 인식.
        for i in range(0, 15):			
            if i == 14 and answer[i] == '.' :	# 문자열 검토가 끝난 뒤에도 문자 끝이 dot인 경우 이를 제거.
                pass
            else:
                real_ans.append(answer[i])
            
    elif length == 2 :			# 검토된 문자열의 길이가 2인 경우, 마지막 문자열을 1번 더 포함시킴.
        real_ans.append(answer[0])
        real_ans.append(answer[1])
        real_ans.append(answer[1])
    elif length == 1 :    			# 검토된 문자열의 길이가 1인 경우, 3개까지 한 글자 반복.
        real_ans.append(answer[0])
        real_ans.append(answer[0])
        real_ans.append(answer[0])
    elif length == 0 : 			# 검토된 문자열의 길이가 0인 경우, 'a' 문자가 3개 이어져야 함.
        real_ans.append('a')
        real_ans.append('a')
        real_ans.append('a')
    else :					# 모든 검사가 끝난 후 이상이 없으면 출력.
        for i in range(0, length):
            real_ans.append(answer[i])
    real_ans = "".join(real_ans)
    return real_ans