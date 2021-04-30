Keywords: interface dialog shell gui x window
From: ���� �����, ��������� ������
Newsgroups: http://gazette.linux.ru.net
Date: Mon, 17 May 2004 18:21:07 +0000 (UTC)
Subject: ���������� ������� ����������� � ������� dialog/Xdialog

��������: http://gazette.linux.ru.net/lg101/sunil.html


   ���������� ������� ����������� � ������� dialog/Xdialog
   �����: Sunil Thomas Thonikuzhiyil (http://linuxgazette.net/authors/sunil.html)
   �������: ���� ����� (http://gazette.linux.ru.net/team/i_pesin.html), 
            ��������� ������ (http://gazette.linux.ru.net/team/a_kuprin.html)

   (�������, ������������� �����, �� ������� ����� � ������ �� ������
   http://gazette.linux.ru.net/lg101/misc/sunil/examples_sh.tar.gz. -- ����. �.�.)


1) ��������
-----------

   ������ ������������� ���������� �������� dialog � Xdialog ���
   ���������� ������� ����������� � ��������. ��� ������������, ��� ��
   ������� � ���������� �������� ���������� ��������������. ���������
   ������ ������ �������� �� ������ http://gnubox.dyndns.org:8080/~sunil/dialog.php.

   dialog ��� ������� ��� ���������� ���������� �����������. Xdialog
   ����������� ��������� ��� X. ��� ��������� �����-����� ���������� �
   ����� ������������� � �������. Dialog ������ � ������ �����������
   ������������� GNU/Linux. ���� �� ������ ������� ţ �� ����������, ��
   ����� ����� ����� �� http://hightek.org/dialog/. ��������� Xdialog
   �������� �� ����� http://xdialog.dyns.net/

   ��� ��������� �������� ���������� � �������� �� ������� ����������
   �������� *nix. ����������� �����ģ���� �������� � ������ �����������
   �������� ���������� ��������, ������������ � ��������� ������
   ��������.


2) ������
---------

   ��� ������ ������, ������ �������� � ��������. �� ������ �������
   ������ � �������� "��" � "���".

#!/bin/bash
DIALOG=${DIALOG=dialog}

$DIALOG --title " ��� ������ ������" --clear \
        --yesno "������! ����� ���� ������ ���������,\n������������ (X)dialog" 10 40

case $? in
    0)
        echo "������� '��'.";;
    1)
        echo "������� '���'.";;
    255)
        echo "������ ������� ESC.";;
esac

   ���������� �����ģ���� ������ � ����, ��������, yesno.sh � ����������
   ������� ����������.

        $chmod u+x yesno.sh

   ������ ���������� ��������� ��� (��.������� [8]1).

        $./yesno.sh

   ������� ������

        DIALOG=${DIALOG=dialog}

   ��
        DIALOG=${DIALOG=Xdialog}

   � �������� ������ �� xterm.

   ������� �������� �����ң� �����ģ���� ���������. ������ ������
   �������� ������������, ������� ����� ���������, ��� ��� ����������
   ��������� ��������� ������������� bash. (������������������ #! � ����
   Unix ���������� sha-bang. ��� ��������� ������� ����� ������
   ������������� ������� ������������ ��� ���������� �������� --
   http://gazette.linux.ru.net/rus/articles/abs-guide/c112.html. -- ����. �.�.)

        DIALOG=${DIALOG=dialog}

   ��� ������ ����������� ���������� DIALOG �������� 'dialog'. ��� ��
   ������ ����������� ��������� �������:
    
       $DIALOG --title " ��� ������ ������" --clear \
            --yesno "������! ����� ���� ������ ���������,\n������������ (X)dialog" 10 40

   ����������� �����:
   --title ������ ��������� �������
   --clear ������� ����� ����� ������������ �������
   --yesno ������ ��� ������� � ����� ��� �����������.

   ��������� ����� ����� ����� � ������� �������. ����� ����������� �
   ����������� �� ������ ����������� ����. ����� ������������ ������ \n
   ��� �������� ��������������� �������� ������. ��������� ��� �����
   ������ ������ � ������ �������. (������� ���� �������� � ��������. ���
   ����� ��� ��� dialog, ��� � Xdialog. ��� ���� ��� ������ ���������
   ���������� Xdialog ���������� ������������ �����. -- ����. �.�.) �����
   �������� ����� ������������ ��� ������ ������� ���������.

   ������ ��������� �ģ� ����������������� ������. � ����������� �� ����,
   ���ͣ�� ������ "��" ��� "���", ��� ���ͣ�� ������� Escape, ����������
   ���������� �������������� $? ����� ��������� ��� ���������� ���������,
   ������� ����� ��� ��� ����� ����������.


2) ���� ������
--------------

   ��������� ��������� ������� ����� ������ � ����� ���������� ţ ��
   ������.

#!/bin/sh
DIALOG=${DIALOG=dialog}
tempfile=`tempfile 2>/dev/null` || tempfile=/tmp/test$$
trap "rm -f $tempfile" 0 1 2 5 15

$DIALOG --title "���� ������" --clear \
        --inputbox "������! ����� ���� ������ ����� �����\n������� ��ϣ ���:" 16 51 2> $tempfile

retval=$?

case $retval in
  0)
    echo "�� ����� `cat $tempfile`"
    ;;
  1)
    echo "����� �� �����.";;
  255)
    if test -s $tempfile ; then
      cat $tempfile
    else
      echo "������ ������� ESC."
    fi
    ;;
esac

   ��������� ��������� � ������� � ��� X (����� ������ dialog �� Xdialog)

   ��� ��������� ������� �������, ��� ����������. ��������� ������
   ���������� ��������� ���� � ��� �������� ��� ���������� ���������:

        tempfile=`mktemp 2>/dev/null` || tempfile=/tmp/test$$
        trap "rm -f $tempfile" 0 1 2 5 15

   (� ������������ ������� ��� ������������ ����� ���������� �����
   �������������� ������� tempfile, �� ����� ���������� �� �������,
   ������� �������� ţ �������� �� mktemp. ���� ������ �������� ����� �
   ����� ������, �.�. � ������ ������ ����������� || ���������
   ������������ ��� ����� ���� /tmp/test$$, ��� $$ -- �������� ����������
   ��������� �����. ����, �� ��� ������, ���������� ���� �� ������������
   ���������� $RANDOM. -- ����. �.�.)

   � ������ ������ �������� ������� ������� ��������� ���� � �������
   ������� mktemp. ���� ��� �� ����������, �� ��������� �������, �
   �������� /tmp. ������ ������ ���������� ���������� ��������. ���
   ���������� ������� (��� �����������, ���������� ��� �� ����������)
   ���������� ������� ��������� ����. ����� -- ��� ������ ��������������
   ��������.

   ����� ����� ���������� ��������� dialog:
        $DIALOG --title "���� ������" --clear \
        --inputbox "������! ����� ���� ������ ����� �����\n������� ��ϣ ���:" 16 51 2> $tempfile

   ��������� �� ��������� ������� ��������� � ���� ������ (stderr - ����.
   �.�.). ��������� ����� �� ������ ����������� ���ģ���� ����� ���
   ����������� ��� ���������.


3) ����������� ����
-------------------

   ��������� ��������� ��������� ��� ������������ ������ � ������������
   ������ ������ �� ���������:

#!/bin/sh
DIALOG=${DIALOG=dialog}
tempfile=`mktemp 2>/dev/null` || tempfile=/tmp/test$$
trap "rm -f $tempfile" 0 1 2 5 15

$DIALOG --clear --title "��� ������� �����������" \
        --menu "��� ����� ����� �����, ������� ���������:" 20 51 4 \
        "Rafi"  "Mohammed Rafi" \
        "Mukesh" "Mukesh" \
        "Kishore" "Kishore Kumar" \
        "Saigal" "K L Saigal" \
        "Lata"  "Lata Mangeshkar" \
        "Yesudas"  "K J Yesudas" 2> $tempfile

retval=$?

choice=`cat $tempfile`

case $retval in
  0)
    echo "�� �� �����! '$choice' -- ��� ������, ��� �� ������� � ����� �����!";;
  1)
    echo "����� �� �����.";;
  255)
    echo "������ ������� ESC.";;
esac

   ������ ������ ������� ���������� ���, ��� ����������� � �������
   inputbox.sh -- ��������� ���������� ������� ���������������� ��
   ��������� ����, ������ �� ����� ���� ���� ��� ���������� ���������.


4) ������ ��������� ������ (radiolist) � ������� (checklist).
-------------------------------------------------------------

   ������������ ����� ������� ���������� ����������� ����, ���������� �
   ���������� �������.

#! /bin/sh
DIALOG=${DIALOG=dialog}
tempfile=`mktemp 2>/dev/null` || tempfile=/tmp/test$$
trap "rm -f $tempfile" 0 1 2 5 15

$DIALOG --backtitle "�� �����������, �������� �������� �����" \
        --title "����� �����������" --clear \
        --radiolist "��� ������� �����, ���... " 20 61 5 \
        "Rafi"  "Mohammed Rafi" off \
        "Lata"    "Lata Mangeshkar" ON \
        "Hemant" "Hemant Kumar" off \
        "Dey"    "MannaDey" off \
        "Kishore"    "Kishore Kumar" off \
        "Yesudas"   "K. J. Yesudas" off  2> $tempfile

retval=$?

choice=`cat $tempfile`
case $retval in
  0)
    echo "���! ��� �� ��� ��������, �� ����� ��� �� '$choice'";;
  1)
    echo "����� �� �����.";;
  255)
    echo "������ ������� ESC.";;
esac

   ��� ����, ����� ������������ ������ �������, ������ �����������,
   �������� � ������� ����� --radiolist �� --checklist.


5) �������� ����������
----------------------

   ����� ������� ��������� ��������������� ������� ���������� ������
   �������:

#!/bin/sh
DIALOG=${DIALOG=dialog}

COUNT=10
(
while test $COUNT != 110
do
echo $COUNT
echo "XXX"
echo "����� ��������� ($COUNT ���������)"
echo "������ 2"
echo "XXX"
COUNT=`expr $COUNT + 10`
sleep 1
done
) |
$DIALOG --title "���������" --gauge "� ��� ������ ����������� ����������" 20 70 0

   ����������� ���������� ���������� ����������� � ���, ��� ���������
   dialog �������� ������ ����� �������� �� ����, ������� �����ޣ� ������
   ������� ������. ���� ��� �������, �� ������� ���������� ��������
   ��������. ������ -- ��� ������������ ������������� ���������� $COUNT.
   ������ �� �ţ dialog/Xdialog ��������� ������� �������� ����������.
   ��� ���� ����������, ����� �������� ���������� ���������� � ���������
   �� 0 �� 100. ������ -- ��� ������������� ����� ���� "XXX" � ��������
   ������������� ���������, ������������ �� �����.

   (� ���������� ����� �������� ���� ������. ���� ������������ dialog, ��
   �ӣ �������������� ���������, � � ������ � Xdialog ������ "������ 2"
   �� ����������� �� ����� ������. ��������������� ���� \n �� ��������.
   -- ����. �.�.)


6) ����� �����
--------------

   ��� ������ ����������� ������� ��� ������ �����:
   
#!/bin/sh
DIALOG=${DIALOG=dialog}

FILE=`$DIALOG --stdout --title "�������� ����" --fselect $HOME/ 10 60`

case $? in
    0)
        echo "������ \"$FILE\"";;
    1)
        echo "����� �� �����.";;
    255)
        echo "������ ������� ESC.";;
esac

   �������� ��������, ��� � ���� ������� ������������ ������ ��������
   ��������� ������ �� dialog. �� ��������� ����������� ���������,
   �������������� � dialog, ���������� �������� ����� stderr, ������� �
   ���������� �������� �������������� ��������������� ������ � stderr �
   ����. ��������� ����� --stdout, ����� ����� �������������� ������ ��
   ����������� �����, ��� � ��������������� � ��������� �������.

   ���������� ���� ��� ������ ����� ������� �� �������. �� ������
   ������������ ����� ���� ��� ������ ������� "Tab". ����� �����, � ���
   ���� ����������� ������� ������ ��������������� � ������ �����,
   ������������� ��� ��������.

   (������ ���� ���� "��", �� ������� ������� �������� ��������. ��
   ������ "��" �� ���������, ���� ���������� ��������� ������ ���������,
   ��������� Xdialog. ����������, ��� ��������
   100%-�� ������������ �� ������ � ������� ���������� -- ����������
   ������ ������ ����. ������ "��" -- ��� ��������� �� ��������� ������.
   � ��������� ������ (dialog) � ���� ��� �� ���������� -- �������
   "Enter" �������������� ��� ������������� ����� � ������������ ţ ���
   ����������� �� ������������ �� �������. � ������� (Xdialog) � ����
   ����� -- ��� �������������� ����� � ����������� �� ������������ ��
   �������� �������. -- ����. �.�.)


7) ��������� � ��������� �����
------------------------------

�) ���������

   ���������� � ����, ������ � ��� ��������� �� ��������� �������. ����
   �������� ���,������ ��� ���� �� �������, ���� ��� �������������, ��
   ������������ ��������� ����. (�������� ������ � dialog. ��� ���������
   ���������� ��������� �������� ���� (��������, �� �� ������� ���)
   Xdialog ������ ��������� �� ������. ������� � �������� ����������
   �������� , ��������, 1000-� ��� �� ��������� -- dialog ������������
   ��� ��� �������� �������� � ��������� ������� ����. Xdialog � ����
   ������ ������ ��������� �� ������. -- ����. �.�.) ��� ���������
   �������� ����� ������������ ������� ���������� ��������, ����
   ��������������� �������� ���������, ������������� � vi ��� ���������
   �� ������: h, j, k � l. (����� ��� dialog. � Xdialog ������������
   ���������� ��� ������ ����� � ������ ��������� �� ���� ������ ��������
   ��� ������ ������ ���������� ��������. -- ����. �.�.) ���� ���
   ��������������� ������ 0, �� �� ��������� ������������ ��������
   �������� ����. ��������� ��������� � ������� ����/�����/���

#!/bin/sh
DIALOG=${DIALOG=dialog}

USERDATE=`$DIALOG --stdout --title "���������" --calendar "�������� ����..." 00 7 7 1981`

case $? in
  0)
    echo "�������: $USERDATE.";;
  1)
    echo "����� �� �����.";;
  255)
    echo "������ ������� ESC.";;
esac


�) ��������� �����

   ���� ������ ��������� ��� �������� �����:

#!/bin/sh

DIALOG=${DIALOG=Xdialog}
USERTIME=`$DIALOG --stdout --title "��������� �����" \
           --timebox "�������,����������, �����..." 0 0 12 34 56`

case $? in
  0)
    echo "������� �����: $USERTIME.";;
  1)
    echo "����� �� �����.";;
  255)
    echo "������ ������� ESC.";;
esac


8) ������ �����������
---------------------

   ����� �����, Xdialog ����������� ������ ����������, ��� �������
   (tree-view), ����� �������� �� ��������� ��������� (range-box),
   �������� ��������� ������ (edit-box) � �.�. �� ��������� �����������
   ����������� �� ������
   http://thgodef.nerim.net/xdialog/doc/box.html. �� ��������
   ��������� � ���������� ����������� ��� dialog -- ��� ��������
   ���������� ���������� � ����� ������������ ��� ���� ������ (password
   box), �������� ����� (tailbox) � �.�. ����� � ��� ���� �����������
   �������������� ������� ����� ����, ����� �����, ��������/������ ���� �
   �.�.

9) ���������
------------

   ��� ������ ������ �������������� ������ ����� ����� dialog � Xdialog,
   ���� � ��� ������ �������� ��������� �����������:

if [ -z $DISPLAY ]
then
    DIALOG=dialog
else
    DIALOG=Xdialog
fi

   ���������� ��������� ������, ������������ ����, � ������� � "�����".

#!/bin/sh
if [ -z $DISPLAY ]
then
    DIALOG=dialog
else
    DIALOG=Xdialog
fi
$DIALOG --yesno "�������, �� ������ ��?" 0 0


10) ������
----------

   1) �������� ����������� ����������� dialog:
   http://hightek.org/dialog/manual-0.9a-20010429.html
     ����������� �������� �� (��� man dialog), ���� ���������� ������
     �������, ��������� dialog.

   2) ������� ��������: http://www.fifi.org/doc/dialog/examples/.

   ��� �������, �������������� �����, �������� �����������������
   ���������, ������� �� ����� ������. ���� �� ����������� Debian
   GNU/Linux, �� ��� ������� �� ���ģ�� � /usr/share/doc/dialog/examples.

   3) �������� Thomas'� Dickey: http://dickey.his.com/dialog/

   4) �������� Vincent'� Stemen'�: http://hightek.org/dialog/.
      ��� �������� �������� ������������� ���������� � ��������� �������
      dialog.

   5) ������������ �� Xdialog:
     http://thgodef.nerim.net/xdialog/doc/index.html.

   �� ���� �������� �� ���ģ�� ������ ���������� � ��������������
   ������������ Xdialog.

Sunil Thomas Thonikuzhiyi

   � ������� ������������� �� �������������� ����������� ���
   ��������������� �������� ����� ������, ����������, �����. �� Linux �
   ������� � 1996. ������� ������ ����������� �� ���������� ������������
   ���� ������������ ������ ����� (Cochin). ����������� ����� ������
   ������������ ������. � ��������� ����� ����� ������� ��������
   ��������� ������.

   Copyright � 2004, Sunil Thomas Thonikuzhiyil. Copying license
   http://linuxgazette.net/copying.html
   Published in Issue 101 of Linux Gazette, April 2004
