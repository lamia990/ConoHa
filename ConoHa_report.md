14/11/13
ConoHa �o�^(������2G�v����)
������������������������������������������������������
User:lamia // Group Wheel�P��
adduser hoge
passwd hoge
�Θb��
������������������������������������������������������
yum update // �ŐV�łւ̍X�V
Port 22 to 10022 // # vi /ect/ssh/sshd_config
		 // # <- �R�����g�A�E�g
		 // 10022�̎g�p�m�F���22�����
������������������������������������������������������
sudoers�ݒ�(wheel��sudo�R�}���h���g����悤��)

$ visudo
/wheel //�t�@�C���������� n�Ŏ��ցB
%wheel        ALL=(ALL)       ALL //�R�����g�A�E�g���O��
������������������������������������������������������
su�y��sudo�R�}���h�`�F�b�N

$ su hoge //hoge�ɐ؂�ւ�
$ sudo echo "hoge"
hoge
$ su //root�ɂȂ��̂��m�F
$ su hoge //�����hoge�ő���
������������������������������������������������������
$ service sshd restart
$ service iptables restart
������������������������������������������������������
//�p�X���[�h�ł̔F�؂��֎~(���J���F�؂̂݋���)
PermitEmptyPasswords no //�R�����g�A�E�g
PasswordAuthentication no //���̂܂�
������������������������������������������������������
Teraterm����ssh�ڑ������݂�����s
 // Port22�ւ̃A�N�Z�X�͒ʂ������APort10022�ւ̃A�N�Z�X�͋���
 // ���F�ؕ����ŏ��񃍃O�C�������݂��̂��p�X�t���[�Y�F�؂ɐ؂�ւ���ƒʂ���(Port22)
 // Port10022�ւ̃A�N�Z�X���ۑ�

URL
http://qiita.com/harapeko_wktk/items/ad4a2e0cb7f00fdfbf0

******************************************************

14/11/14
Teraterm����̐ڑ����ēx���݂�����s
iptables��������Βʂ邱�Ƃ�����

/etc/sysconfig/iptables
-A INPUT -p tcp -m tcp --dport 10022 -j ACCEPT
����ǋL

���̌�sshd_config�ɂ�
Port10022��ʂ�

���sshd��iptables��restart

URL
http://qa.atmarkit.co.jp/q/3164
������������������������������������������������������

