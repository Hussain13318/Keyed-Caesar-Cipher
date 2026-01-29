INCLUDE Irvine32.inc

.data
; --------------------------- BIG BANNER (CORRECTED) ---------------------------
    big_title   BYTE "+-------------------------------------------------------------------------------+", 0ah, 0dh
                BYTE "|  _  __  _____ __   __ _____  ____      ____    _    _____ ____    _    ____   |", 0ah, 0dh
                BYTE "| | |/ / | ____|\ \ / /| ____||  _ \    / ___|  / \  | ____/ ___|  / \  |  _ \  |", 0ah, 0dh
                BYTE "| | ' /  |  _|   \ V / |  _|  | | | |  | |     / _ \ |  _| \___ \ / _ \ | |_) | |", 0ah, 0dh
                BYTE "| | . \  | |___   | |  | |___ | |_| |  | |___ / ___ \| |___ ___) / ___ \|  _ <  |", 0ah, 0dh
                BYTE "| |_|\_\ |_____|  |_|  |_____||____/    \____/_/   \_\_____|____/_/   \_\_| \_\ |", 0ah, 0dh
                BYTE "|                                                                               |", 0ah, 0dh
                BYTE "|                ____ ___ ____  _   _ _____ ____                                |", 0ah, 0dh
                BYTE "|               / ___|_ _|  _ \| | | | ____|  _ \                               |", 0ah, 0dh
                BYTE "|              | |    | || |_) | |_| |  _| | |_) |                              |", 0ah, 0dh
                BYTE "|              | |___ | ||  __/|  _  | |___|  _ <                               |", 0ah, 0dh
                BYTE "|               \____|___|_|   |_| |_|_____|_| \_\                              |", 0ah, 0dh
                BYTE "+-------------------------------------------------------------------------------+", 0ah, 0dh, 0

    ; Corrected the spelling in the string too


    ; --------------------------- ASCII UI BOXES ---------------------------
    box_menu    BYTE 0ah, 0dh, "=======================================", 0ah, 0dh
                BYTE "||            MAIN  MENU             ||", 0ah, 0dh
                BYTE "=======================================", 0ah, 0dh, 0

    box_enc_txt BYTE 0ah, 0dh, "---------------------------------------", 0ah, 0dh
                BYTE "|         ENCRYPTING  TEXT            |", 0ah, 0dh
                BYTE "---------------------------------------", 0ah, 0dh, 0

    box_dec_txt BYTE 0ah, 0dh, "---------------------------------------", 0ah, 0dh
                BYTE "|          DECRYPTING  TEXT           |", 0ah, 0dh
                BYTE "---------------------------------------", 0ah, 0dh, 0

    box_enc_fil BYTE 0ah, 0dh, "[!]---------------------------------[!]", 0ah, 0dh
                BYTE "[!]        ENCRYPTING  FILE         [!]", 0ah, 0dh
                BYTE "[!]---------------------------------[!]", 0ah, 0dh, 0

    box_dec_fil BYTE 0ah, 0dh, "[?]---------------------------------[?]", 0ah, 0dh
                BYTE "[?]        DECRYPTING  FILE         [?]", 0ah, 0dh
                BYTE "[?]---------------------------------[?]", 0ah, 0dh, 0

    box_history BYTE 0ah, 0dh, "_______________________________________", 0ah, 0dh
                BYTE "|         VIEW CIPHER HISTORY         |", 0ah, 0dh
                BYTE "|_____________________________________|", 0ah, 0dh, 0

    box_exit    BYTE 0ah, 0dh, "x-------------------------------------x", 0ah, 0dh
                BYTE "x          EXITING PROGRAM            x", 0ah, 0dh
                BYTE "x-------------------------------------x", 0ah, 0dh, 0

    ; ------------------------------ MESSAGES ------------------------------
    encryption_message      BYTE "Welcome to KEYED CAESER CIPHER Program!",0
    menu                    BYTE 0ah, 0dh, "--- Main Menu ---", 0ah, 0dh, 0
    menu_options            BYTE "1. Encrypt Text", 0ah, 0dh, "2. Decrypt Text", 0ah, 0dh,
                                 "3. Encrypt File", 0ah, 0dh, "4. Decrypt File", 0ah, 0dh, 
                                 "5. View Cipher History", 0ah, 0dh, "6. Exit Program", 0ah, 0dh, 0
    choice_prompt           BYTE "Enter your choice (1-6): ", 0
    invalid_choice_msg      BYTE 0ah, 0dh, "Error: Invalid choice! Please enter 1-6.", 0ah, 0dh, 0

    user_input_prompt       BYTE "Enter plaintext to encrypt: ",0
    enter_ciphertext_msg    BYTE "Enter ciphertext to decrypt: ", 0
    enter_key_message       BYTE "Enter encryption key: ",0
    enter_shift_message     BYTE "Enter shift value: ",0

    input_file_prompt       BYTE "Enter input filename: ", 0
    output_file_prompt      BYTE "Enter output filename: ", 0
    file_success_msg        BYTE "File processed successfully!", 0ah, 0dh, 0
    file_read_error_msg     BYTE "Error: Could not read input file!", 0ah, 0dh, 0
    file_write_error_msg    BYTE "Error: Could not write to output file!", 0ah, 0dh, 0
    file_processing_msg     BYTE "Processing file...", 0ah, 0dh, 0
    history_header          BYTE 0ah, 0dh, "--- Cipher History ---", 0ah, 0dh, 0
    history_not_found       BYTE "No history found or could not read history file.", 0ah, 0dh, 0

    confirm_msg_string      BYTE "Your entered string is: ",0
    confirm_msg_key         BYTE "Your entered key is: ",0
    confirm_msg_shift       BYTE "Your Entered shift value is: ", 0

    err_msg_not_digit       BYTE "Error: Invalid input! Shift value must be a DIGIT ", 0ah, 0dh, 0
    err_msg_not_alpha       BYTE "Error: Invalid input! Please enter only English Alphabets", 0ah, 0dh, 0
    err_msg_out_of_range    BYTE "Error: Invalid input! Please enter the value from 0 to 26", 0ah, 0dh, 0

    encryption_started_msg  BYTE 0ah,0dh,"!--- Lets start encryption ---!",0
    decryption_started_msg  BYTE 0ah,0dh,"--- Decryption Started ---",0
    alphabet_label          BYTE "Keyed alphabet: ", 0
    encrypted_message_label BYTE "Encrypted message: ", 0
    decrypted_message_label BYTE "Decrypted message: ", 0

    user_entered_string     BYTE 100 DUP(0)
    user_key_string         BYTE 100 DUP(0)
    shift_buffer            BYTE 20 DUP(0)
    shift_value             DWORD 0
    cipher_alphabet         BYTE 27 DUP(0)
    used_letters            BYTE 26 DUP(0)
    input_filename          BYTE 100 DUP(0)
    output_filename         BYTE 100 DUP(0)
    file_buffer             BYTE 5000 DUP(0)
    bytes_read              DWORD ?
    bytes_written           DWORD ?
    history_filename        BYTE "cipher_history.txt", 0
    history_buffer          BYTE 500 DUP(0)
    operation_type          BYTE 20 DUP(0)

.code
; ------------------- PROCEDURES (SAME LOGIC) -------------------
alphabet_chek PROC uses eax esi
check_loop:
    mov al, [esi]
    cmp al, 0
    je valid_string
    cmp al, 32
    je next_iteration
    cmp al, 'A'
    jb invalid_char_found
    cmp al, 'Z'
    jbe next_iteration
    cmp al, 'a'
    jb invalid_char_found
    cmp al, 'z'
    ja invalid_char_found
next_iteration:
    inc esi
    jmp check_loop
invalid_char_found:
    or al, 1
    ret
valid_string:
    cmp al, al
    ret
alphabet_chek ENDP

digit_chek PROC USES eax esi
checking_loop:
    mov al, [esi]
    cmp al, 0
    je valid_digit
    cmp al, '0'
    jb invalid_digit
    cmp al, '9'
    ja invalid_digit
    inc esi
    jmp checking_loop
invalid_digit:
    or al, 1
    ret
valid_digit:
    cmp al, al
    ret
digit_chek ENDP

KeyedAlphabets PROC
    push esi
    push edi
    push ecx
    push edx
    mov ecx, 26
    mov edi, OFFSET used_letters
    mov al, 0
clearing:
    mov [edi], al
    inc edi
    loop clearing
    mov edi, OFFSET cipher_alphabet
    mov esi, OFFSET user_key_string
AddFromKey:
    mov al, [esi]
    test al, al
    jz AddMissingLetters
    and al, 11011111b
    cmp al, 'A'
    jb NextChar
    cmp al, 'Z'
    ja NextChar
    movzx edx, al
    sub edx, 'A'
    cmp byte PTR [used_letters + edx], 1
    je NextChar
    mov [edi], al
    inc edi
    mov byte PTR [used_letters + edx], 1
NextChar:
    inc esi
    jmp AddFromKey
AddMissingLetters:
    mov al, 'A'
AddLoop:
    movzx edx, al
    sub edx, 'A'
    cmp byte PTR [used_letters + edx], 0
    jne SkipLetter
    mov [edi], al
    inc edi
SkipLetter:
    inc al
    cmp al, 'Z' + 1
    jne AddLoop
    mov byte PTR [edi], 0
    pop edx
    pop ecx
    pop edi
    pop esi
    ret
KeyedAlphabets ENDP

EncryptMessage PROC
    push esi
    push edi
    push ebx
    mov esi, OFFSET user_entered_string
    mov edi, OFFSET user_entered_string
    mov ebx, shift_value
encrypt_loop:
    mov al, [esi]
    test al, al
    jz encryption_done
    cmp al, 'A'
    jb check_lowercase
    cmp al, 'Z'
    jbe uppercase
check_lowercase:
    cmp al, 'a'
    jb skip_char
    cmp al, 'z'
    ja skip_char
    and al, 11011111b
uppercase:
    sub al, 'A'
    add al, bl
    cmp al, 26
    jl index_mod_done
    sub al, 26
index_mod_done:
    movzx edx, al
    mov al, [cipher_alphabet + edx]
    mov [edi], al
    inc esi
    inc edi
    jmp encrypt_loop
skip_char:
    mov [edi], al
    inc esi
    inc edi
    jmp encrypt_loop
encryption_done:
    mov BYTE PTR [edi], 0
    pop ebx
    pop edi
    pop esi
    ret
EncryptMessage ENDP

DecryptMessage PROC
    push esi
    push edi
    push ebx
    push ecx
    push edx
    mov ebx, shift_value
    mov esi, OFFSET user_entered_string
    mov edi, OFFSET user_entered_string
decrypt_loop:
    mov al, [esi]
    test al, al
    jz decryption_done
    mov dl, al
    and dl, 11011111b
    cmp dl, 'A'
    jb dec_skip_char
    cmp dl, 'Z'
    ja dec_skip_char
    mov ecx, 0
    mov edx, OFFSET cipher_alphabet
find_in_keyed_alpha:
    cmp byte PTR [edx], 0
    jz dec_skip_char
    mov ah, [esi]
    and ah, 11011111b
    cmp ah, [edx]
    je found_keyed_index
    inc ecx
    inc edx
    jmp find_in_keyed_alpha
found_keyed_index:
    sub ecx, ebx
    cmp ecx, 0
    jge pos_index
    add ecx, 26
pos_index:
    mov eax, ecx
    add al, 'A'
    mov [edi], al
    inc esi
    inc edi
    jmp decrypt_loop
dec_skip_char:
    mov [edi], al
    inc esi
    inc edi
    jmp decrypt_loop
decryption_done:
    mov BYTE PTR [edi], 0
    pop edx
    pop ecx
    pop ebx
    pop edi
    pop esi
    ret
DecryptMessage ENDP

ReadFileContent PROC
    LOCAL fileHandle:DWORD
    INVOKE CreateFile, OFFSET input_filename, GENERIC_READ, FILE_SHARE_READ, NULL, OPEN_EXISTING, FILE_ATTRIBUTE_NORMAL, 0
    mov fileHandle, eax
    cmp eax, INVALID_HANDLE_VALUE
    je read_error
    INVOKE ReadFile, fileHandle, OFFSET file_buffer, 4999, OFFSET bytes_read, 0
    INVOKE CloseHandle, fileHandle
    mov eax, bytes_read
    mov byte PTR [file_buffer + eax], 0
    clc
    ret
read_error:
    stc
    ret
ReadFileContent ENDP

WriteFileContent PROC
    LOCAL fileHandle:DWORD
    INVOKE CreateFile, OFFSET output_filename, GENERIC_WRITE, 0, NULL, CREATE_ALWAYS, FILE_ATTRIBUTE_NORMAL, 0
    mov fileHandle, eax
    cmp eax, INVALID_HANDLE_VALUE
    je write_error
    INVOKE WriteFile, fileHandle, OFFSET file_buffer, bytes_read, OFFSET bytes_written, 0
    INVOKE CloseHandle, fileHandle
    clc
    ret
write_error:
    stc
    ret
WriteFileContent ENDP

SaveToHistory PROC
    LOCAL fileHandle:DWORD
    LOCAL histLen:DWORD
    push esi
    push edi
    push edx
    push ecx
    push eax
    mov esi, OFFSET history_buffer
    mov edi, esi
    mov edx, OFFSET operation_type
    call StrLength
    mov ecx, eax
    mov edx, OFFSET operation_type
copy_op:
    mov al, [edx]
    mov [edi], al
    inc edx
    inc edi
    loop copy_op
    mov al, '|'
    mov [edi], al
    inc edi
    mov al, ' '
    mov [edi], al
    inc edi
    mov edx, OFFSET user_key_string
    call StrLength
    mov ecx, eax
    mov edx, OFFSET user_key_string
copy_key:
    mov al, [edx]
    mov [edi], al
    inc edx
    inc edi
    loop copy_key
    mov al, '|'
    mov [edi], al
    inc edi
    mov al, ' '
    mov [edi], al
    inc edi
    mov al, 0ah
    mov [edi], al
    inc edi
    mov al, 0dh
    mov [edi], al
    inc edi
    mov al, 0
    mov [edi], al
    mov eax, edi
    sub eax, OFFSET history_buffer
    mov histLen, eax
    INVOKE CreateFile, OFFSET history_filename, GENERIC_WRITE, 0, NULL, OPEN_ALWAYS, FILE_ATTRIBUTE_NORMAL, 0
    mov fileHandle, eax
    cmp eax, INVALID_HANDLE_VALUE
    je history_error
    INVOKE SetFilePointer, fileHandle, 0, 0, FILE_END
    INVOKE WriteFile, fileHandle, OFFSET history_buffer, histLen, OFFSET bytes_written, 0
    INVOKE CloseHandle, fileHandle
history_error:
    pop eax
    pop ecx
    pop edx
    pop edi
    pop esi
    ret
SaveToHistory ENDP

ViewHistory PROC
    LOCAL fileHandle:DWORD
    mov eax,13
    call SetTextColor
    mov edx, OFFSET history_header
    call WriteString
    mov eax,14
    call SetTextColor
    INVOKE CreateFile, OFFSET history_filename, GENERIC_READ, FILE_SHARE_READ, NULL, OPEN_EXISTING, FILE_ATTRIBUTE_NORMAL, 0
    mov fileHandle, eax
    cmp eax, INVALID_HANDLE_VALUE
    je no_history
    INVOKE ReadFile, fileHandle, OFFSET file_buffer, 4999, OFFSET bytes_read, 0
    INVOKE CloseHandle, fileHandle
    cmp bytes_read, 0
    je no_history
    mov eax, bytes_read
    mov byte PTR [file_buffer + eax], 0
    mov edx, OFFSET file_buffer
    call WriteString
    call Crlf
    ret
no_history:
    mov edx, OFFSET history_not_found
    call WriteString
    ret
ViewHistory ENDP

;-------------- MAIN PROCEDURE ------------------
main PROC
    mov eax,13               ;dark bkue
    call SetTextColor

    mov edx,OFFSET big_title
    call WriteString
    call Crlf 

    mov eax, 14             ; yellow Welcome
    call SetTextColor
    mov edx, OFFSET encryption_message
    call WriteString
    call Crlf

menu_loop:
    call Crlf ; Extra space for scrolling
    mov eax, 11              ;  Cyan Menu Box
    call SetTextColor
    mov edx, OFFSET box_menu
    call WriteString
    
    mov edx, OFFSET menu
    call WriteString
    mov eax, 15 ; White Menu Text
    call SetTextColor

    mov edx, OFFSET menu_options
    call WriteString

    mov eax,14
    call SetTextColor
    mov edx, OFFSET choice_prompt
    call WriteString

    call ReadInt
    
    cmp eax, 1
    je EncryptFlow
    cmp eax, 2
    je DecryptFlow
    cmp eax, 3
    je EncryptFileFlow
    cmp eax, 4
    je DecryptFileFlow
    cmp eax, 5
    je HistoryFlow
    cmp eax, 6
    je ExitProgram

    ; Invalid Input Logic
    mov eax, 4 ; Red Error
    call SetTextColor
    mov edx, OFFSET invalid_choice_msg
    call WriteString
    call Crlf
    jmp menu_loop

;-------------- 1. ENCRYPT FLOW ------------------
EncryptFlow:
    call Crlf
    mov eax, 6 ; Green Header
    call SetTextColor
    mov edx, OFFSET box_enc_txt
    call WriteString

plaintext_encryption:
    mov eax, 15 ; White Prompts
    call SetTextColor
    mov edx, OFFSET user_input_prompt
    call WriteString
    mov edx, OFFSET user_entered_string
    mov ecx, 100
    call ReadString
    
    mov esi, OFFSET user_entered_string
    call alphabet_chek
    jz encryption_checking

    mov eax, 4 ; Red Error
    call SetTextColor
    mov edx, OFFSET err_msg_not_alpha
    call WriteString
    jmp plaintext_encryption

encryption_checking:
    mov edx, OFFSET confirm_msg_string
    call WriteString
    mov edx, OFFSET user_entered_string
    call WriteString
    call Crlf

encryption_key_getting:
    mov edx, OFFSET enter_key_message
    call WriteString
    mov edx, OFFSET user_key_string
    mov ecx, 50
    call ReadString

    mov esi, OFFSET user_key_string
    call alphabet_chek
    jz checking_key
    mov eax, 12 ; Red
    call SetTextColor
    mov edx, OFFSET err_msg_not_alpha
    call WriteString
    mov eax, 15
    call SetTextColor
    jmp encryption_key_getting

checking_key:
    mov edx, OFFSET confirm_msg_key
    call WriteString
    mov edx, OFFSET user_key_string
    call WriteString
    call Crlf

shift_value_getting:
    mov edx, OFFSET enter_shift_message
    call WriteString
    mov edx, OFFSET shift_buffer
    mov ecx, 19
    call ReadString

    mov esi, OFFSET shift_buffer
    call digit_chek
    jz checking_shift
    mov eax, 12
    call SetTextColor
    mov edx, OFFSET err_msg_not_digit
    call WriteString
    mov eax, 15
    call SetTextColor
    jmp shift_value_getting

checking_shift:
    mov edx, OFFSET shift_buffer
    call ParseDecimal32
    mov shift_value, eax
    cmp eax, 0
    jl invalid_range_enc
    cmp eax, 26
    jg invalid_range_enc
    jmp valid_shift_enc

invalid_range_enc:
    mov eax, 12
    call SetTextColor
    mov edx, OFFSET err_msg_out_of_range
    call WriteString
    mov eax, 15
    call SetTextColor
    jmp shift_value_getting

valid_shift_enc:    
    mov edx, OFFSET confirm_msg_shift
    call WriteString
    mov eax, shift_value
    call WriteDec
    call Crlf

    mov eax, 10 ; Green status
    call SetTextColor
    mov edx, OFFSET encryption_started_msg
    call WriteString
    call Crlf

    mov eax,14
    call SetTextColor
    call KeyedAlphabets
    mov edx, OFFSET alphabet_label
    call WriteString
    mov edx, OFFSET cipher_alphabet
    call WriteString
    call Crlf
    call EncryptMessage
    mov edx, OFFSET encrypted_message_label
    call WriteString
    mov edx, OFFSET user_entered_string
    call WriteString
    call Crlf
    mov eax,15
    call SetTextColor

    mov esi, OFFSET operation_type
    mov byte PTR [esi], 'E'
    mov byte PTR [esi+1], 'n'
    mov byte PTR [esi+2], 'c'
    mov byte PTR [esi+3], 'r'
    mov byte PTR [esi+4], 'y'
    mov byte PTR [esi+5], 'p'
    mov byte PTR [esi+6], 't'
    mov byte PTR [esi+7], 0
    call SaveToHistory
    jmp menu_loop

;-------------- 2. DECRYPT FLOW ------------------
DecryptFlow:
    call Crlf
    mov eax, 1 ; Yellow Header
    call SetTextColor
    mov edx, OFFSET box_dec_txt
    call WriteString

ciphertext_getting:
    mov eax, 15 ; White Prompts
    call SetTextColor
    mov edx, OFFSET enter_ciphertext_msg
    call WriteString
    mov edx, OFFSET user_entered_string
    mov ecx, 100
    call ReadString

    mov esi, OFFSET user_entered_string
    call alphabet_chek
    jz ciphertext_checking
    mov eax, 12 ; Red
    call SetTextColor
    mov edx, OFFSET err_msg_not_alpha
    call WriteString
    jmp ciphertext_getting

ciphertext_checking:
    mov edx, OFFSET confirm_msg_string
    call WriteString
    mov edx, OFFSET user_entered_string
    call WriteString
    call Crlf

decryption_key_getting:
    mov edx, OFFSET enter_key_message
    call WriteString
    mov edx, OFFSET user_key_string
    mov ecx, 50
    call ReadString
    mov esi, OFFSET user_key_string
    call alphabet_chek
    jz dec_key_checking
    mov eax, 12
    call SetTextColor
    mov edx, OFFSET err_msg_not_alpha
    call WriteString
    mov eax, 15
    call SetTextColor
    jmp decryption_key_getting

dec_key_checking:
    mov edx, OFFSET confirm_msg_key
    call WriteString
    mov edx, OFFSET user_key_string
    call WriteString
    call Crlf

getting_shift:
    mov edx, OFFSET enter_shift_message
    call WriteString
    mov edx, OFFSET shift_buffer
    mov ecx, 19
    call ReadString
    mov esi, OFFSET shift_buffer
    call digit_chek
    jz shift_value_checking
    mov eax, 12
    call SetTextColor
    mov edx, OFFSET err_msg_not_digit
    call WriteString
    mov eax, 15
    call SetTextColor
    jmp getting_shift

shift_value_checking:
    mov edx, OFFSET shift_buffer
    call ParseDecimal32
    mov shift_value, eax
    cmp eax, 0
    jl invalid_range_dec
    cmp eax, 26
    jg invalid_range_dec
    jmp valid_shift_dec

invalid_range_dec:
    mov eax, 12
    call SetTextColor
    mov edx, OFFSET err_msg_out_of_range
    call WriteString
    mov eax, 15
    call SetTextColor
    jmp getting_shift

valid_shift_dec: 
    mov edx, OFFSET confirm_msg_shift
    call WriteString
    mov eax, shift_value
    call WriteDec
    call Crlf

    mov eax, 12 ; light red status
    call SetTextColor
    mov edx, OFFSET decryption_started_msg
    call WriteString
    call Crlf
    mov eax,14
    call SetTextColor
    call KeyedAlphabets
    mov edx, OFFSET alphabet_label
    call WriteString
    mov edx, OFFSET cipher_alphabet
    call WriteString
    call Crlf
    call DecryptMessage
    mov edx, OFFSET decrypted_message_label
    call WriteString
    mov edx, OFFSET user_entered_string
    call WriteString
    call Crlf

    mov esi, OFFSET operation_type
    mov byte PTR [esi], 'D'
    mov byte PTR [esi+1], 'e'
    mov byte PTR [esi+2], 'c'
    mov byte PTR [esi+3], 'r'
    mov byte PTR [esi+4], 'y'
    mov byte PTR [esi+5], 'p'
    mov byte PTR [esi+6], 't'
    mov byte PTR [esi+7], 0
    call SaveToHistory
    jmp menu_loop

;-------------- 3. ENCRYPT FILE FLOW ------------------
EncryptFileFlow:
    call Crlf
    mov eax, 6 ; Green Header
    call SetTextColor
    mov edx, OFFSET box_enc_fil
    call WriteString
    mov eax, 15 ; White
    call SetTextColor

    mov edx, OFFSET input_file_prompt
    call WriteString
    mov edx, OFFSET input_filename
    mov ecx, 99
    call ReadString

    mov edx, OFFSET output_file_prompt
    call WriteString
    mov edx, OFFSET output_filename
    mov ecx, 99
    call ReadString

enc_file_key:
    mov edx, OFFSET enter_key_message
    call WriteString
    mov edx, OFFSET user_key_string
    mov ecx, 50
    call ReadString
    mov esi, OFFSET user_key_string
    call alphabet_chek
    jz enc_file_shift
    mov eax, 12
    call SetTextColor
    mov edx, OFFSET err_msg_not_alpha
    call WriteString
    mov eax, 15
    call SetTextColor
    jmp enc_file_key

enc_file_shift:
    mov edx, OFFSET enter_shift_message
    call WriteString
    mov edx, OFFSET shift_buffer
    mov ecx, 19
    call ReadString
    mov esi, OFFSET shift_buffer
    call digit_chek
    jz enc_file_valid_shift
    mov eax, 12
    call SetTextColor
    mov edx, OFFSET err_msg_not_digit
    call WriteString
    mov eax, 15
    call SetTextColor
    jmp enc_file_shift

enc_file_valid_shift:
    mov edx, OFFSET shift_buffer
    call ParseDecimal32
    mov shift_value, eax
    cmp eax, 0
    jl enc_file_invalid_range
    cmp eax, 26
    jg enc_file_invalid_range
    jmp enc_file_process

enc_file_invalid_range:
    mov eax, 12
    call SetTextColor
    mov edx, OFFSET err_msg_out_of_range
    call WriteString
    mov eax, 15
    call SetTextColor
    jmp enc_file_shift

enc_file_process:

    mov eax, 14
    call SetTextColor
    mov edx, OFFSET file_processing_msg
    call WriteString
    mov eax, 10
    call SetTextColor
    call ReadFileContent
    jc enc_file_read_err

    call KeyedAlphabets
    mov esi, OFFSET file_buffer
    mov edi, OFFSET user_entered_string
    mov ecx, 99
copy_to_string:
    mov al, [esi]
    mov [edi], al
    test al, al
    jz enc_file_copied
    inc esi
    inc edi
    loop copy_to_string

enc_file_copied:
    call EncryptMessage
    mov esi, OFFSET user_entered_string
    mov edi, OFFSET file_buffer
copy_to_buffer:
    mov al, [esi]
    mov [edi], al
    test al, al
    jz enc_file_done_copy
    inc esi
    inc edi
    jmp copy_to_buffer

enc_file_done_copy:
    call WriteFileContent
    jc enc_file_write_err
    mov edx, OFFSET file_success_msg
    call WriteString

    mov esi, OFFSET operation_type
    mov byte PTR [esi], 'F'
    mov byte PTR [esi+1], 'i'
    mov byte PTR [esi+2], 'l'
    mov byte PTR [esi+3], 'e'
    mov byte PTR [esi+4], ' '
    mov byte PTR [esi+5], 'E'
    mov byte PTR [esi+6], 'n'
    mov byte PTR [esi+7], 'c'
    mov byte PTR [esi+8], 0
    call SaveToHistory
    jmp menu_loop

enc_file_read_err:
    mov eax, 4
    call SetTextColor
    mov edx, OFFSET file_read_error_msg
    call WriteString
    jmp menu_loop

enc_file_write_err:
    mov eax, 4
    call SetTextColor
    mov edx, OFFSET file_write_error_msg
    call WriteString
    jmp menu_loop

;-------------- 4. DECRYPT FILE FLOW ------------------
DecryptFileFlow:
    call Crlf
    mov eax, 1 ; Yellow Header
    call SetTextColor
    mov edx, OFFSET box_dec_fil
    call WriteString
    mov eax, 15 ; White
    call SetTextColor

    mov edx, OFFSET input_file_prompt
    call WriteString
    mov edx, OFFSET input_filename
    mov ecx, 99
    call ReadString

    mov edx, OFFSET output_file_prompt
    call WriteString
    mov edx, OFFSET output_filename
    mov ecx, 99
    call ReadString

dec_file_key:
    mov edx, OFFSET enter_key_message
    call WriteString
    mov edx, OFFSET user_key_string
    mov ecx, 50
    call ReadString
    mov esi, OFFSET user_key_string
    call alphabet_chek
    jz dec_file_shift
    mov eax, 12
    call SetTextColor
    mov edx, OFFSET err_msg_not_alpha
    call WriteString
    mov eax, 15
    call SetTextColor
    jmp dec_file_key

dec_file_shift:
    mov edx, OFFSET enter_shift_message
    call WriteString
    mov edx, OFFSET shift_buffer
    mov ecx, 19
    call ReadString
    mov esi, OFFSET shift_buffer
    call digit_chek
    jz dec_file_valid_shift
    mov eax, 12
    call SetTextColor
    mov edx, OFFSET err_msg_not_digit
    call WriteString
    mov eax, 15
    call SetTextColor
    jmp dec_file_shift

dec_file_valid_shift:
    mov edx, OFFSET shift_buffer
    call ParseDecimal32
    mov shift_value, eax
    cmp eax, 0
    jl dec_file_invalid_range
    cmp eax, 26
    jg dec_file_invalid_range
    jmp dec_file_process

dec_file_invalid_range:
    mov eax, 12
    call SetTextColor
    mov edx, OFFSET err_msg_out_of_range
    call WriteString
    mov eax, 15
    call SetTextColor
    jmp dec_file_shift

dec_file_process:
    mov eax, 14
    call SetTextColor
    mov edx, OFFSET file_processing_msg
    call WriteString
    mov eax, 12
    call SetTextColor
    call ReadFileContent
    jc dec_file_read_err
    call KeyedAlphabets
    mov esi, OFFSET file_buffer
    mov edi, OFFSET user_entered_string
    mov ecx, 99
dec_copy_to_string:
    mov al, [esi]
    mov [edi], al
    test al, al
    jz dec_file_copied
    inc esi
    inc edi
    loop dec_copy_to_string

dec_file_copied:
    call DecryptMessage
    mov esi, OFFSET user_entered_string
    mov edi, OFFSET file_buffer
dec_copy_to_buffer:
    mov al, [esi]
    mov [edi], al
    test al, al
    jz dec_file_done_copy
    inc esi
    inc edi
    jmp dec_copy_to_buffer

dec_file_done_copy:
    call WriteFileContent
    jc dec_file_write_err
    mov edx, OFFSET file_success_msg
    call WriteString

    mov esi, OFFSET operation_type
    mov byte PTR [esi], 'F'
    mov byte PTR [esi+1], 'i'
    mov byte PTR [esi+2], 'l'
    mov byte PTR [esi+3], 'e'
    mov byte PTR [esi+4], ' '
    mov byte PTR [esi+5], 'D'
    mov byte PTR [esi+6], 'e'
    mov byte PTR [esi+7], 'c'
    mov byte PTR [esi+8], 0
    call SaveToHistory
    jmp menu_loop

dec_file_read_err:
    mov eax, 4
    call SetTextColor
    mov edx, OFFSET file_read_error_msg
    call WriteString
    jmp menu_loop

dec_file_write_err:
    mov eax, 4
    call SetTextColor
    mov edx, OFFSET file_write_error_msg
    call WriteString
    jmp menu_loop

;-------------- 5. HISTORY FLOW ---------------------
HistoryFlow:
    call Crlf
    mov eax, 13 ; Light Magenta Header
    call SetTextColor
    mov edx, OFFSET box_history
    call WriteString
    mov eax, 15
    call SetTextColor
    call ViewHistory
    jmp menu_loop

;------------- 6. EXIT PROGRAM ----------------------
ExitProgram:
    call Crlf
    mov eax, 12 ; Red
    call SetTextColor
    mov edx, OFFSET box_exit
    call WriteString
    mov eax,15
    call SetTextColor

    INVOKE ExitProcess, 0

main ENDP
END main