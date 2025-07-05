
## 🛠️ Steps & Commands
# 🚀 DevOps EC2 CLI Project

مشروع عملي لإنشاء وإدارة EC2 Instance باستخدام AWS CLI فقط.  
المشروع بيشرح خطوة بخطوة إزاي تنشئ Key Pair، وSecurity Group، وتشغّل وتوقف EC2 Instance من التيرمنال.

---

## 🛠️ الأوامر المستخدمة

```bash
# إنشاء مفتاح SSH بصيغة PPK وتخزينه في ملف
aws ec2 create-key-pair --key-name devops90-cli-key --key-format ppk --query 'KeyMaterial' --output text > devops90-cli-key.ppk

# إنشاء Security Group جديد
aws ec2 create-security-group --group-name devops90-sg --description 'from cli' --query 'GroupId'

# فتح منفذ SSH (بروتوكول TCP على البورت 22) داخل الـ Security Group
aws ec2 authorize-security-group-ingress --group-id sg-05fcdbf822946a6dc --protocol tcp --port 22 --cidr 172.31.0.0/16

# تشغيل EC2 Instance باستخدام AMI و Security Group و Key Pair
aws ec2 run-instances \
    --image-id ami-09e1162c87f73958b \
    --count 1 \
    --instance-type t3.micro \
    --key-name devops90-cli-key \
    --region eu-north-1 \
    --security-group-ids sg-05fcdbf822946a6dc \
    --tag-specifications "ResourceType=instance,Tags=[{Key=env,Value=devops},{Key=name,Value=devops-cli}]"

# إنهاء (Terminate) الـ EC2 Instance
aws ec2 terminate-instances --instance-ids i-0fea6bd081265dceb


📁 الملفات
devops90-cli-key.ppk: مفتاح SSH الخاص بالاتصال بالإنستانس.

README.md: شرح كل خطوات المشروع.

🧠 ملاحظات
غير sg-05fcdbf822946a6dc و i-0fea6bd081265dceb لو الـ IDs عندك مختلفة.

اتأكد إن AWS CLI متثبت ومظبط (aws configure) قبل تنفيذ الأوامر.




