# jianxiu
管理信息系统作业
一、sql语句
/*!40101 SET @OLD_CHARACTER_SET_CLIENT=@@CHARACTER_SET_CLIENT */;
/*!40101 SET @OLD_CHARACTER_SET_RESULTS=@@CHARACTER_SET_RESULTS */;
/*!40101 SET @OLD_COLLATION_CONNECTION=@@COLLATION_CONNECTION */;
/*!40101 SET NAMES utf8 */;
/*!40103 SET @OLD_TIME_ZONE=@@TIME_ZONE */;
/*!40103 SET TIME_ZONE='+00:00' */;
/*!40014 SET @OLD_UNIQUE_CHECKS=@@UNIQUE_CHECKS, UNIQUE_CHECKS=0 */;
/*!40014 SET @OLD_FOREIGN_KEY_CHECKS=@@FOREIGN_KEY_CHECKS, FOREIGN_KEY_CHECKS=0 */;
/*!40101 SET @OLD_SQL_MODE=@@SQL_MODE, SQL_MODE='NO_AUTO_VALUE_ON_ZERO' */;
/*!40111 SET @OLD_SQL_NOTES=@@SQL_NOTES, SQL_NOTES=0 */;

--
-- Table structure for table `baoyangjilu`
--

DROP TABLE IF EXISTS `baoyangjilu`;
/*!40101 SET @saved_cs_client     = @@character_set_client */;
/*!40101 SET character_set_client = utf8 */;
CREATE TABLE `baoyangjilu` (
  `id` int(11) NOT NULL,
  `保养时间` datetime DEFAULT NULL,
  `完成情况` varchar(255) DEFAULT NULL,
  `保养项目id` int(11) DEFAULT NULL,
  `保养人ID` int(11) DEFAULT NULL,
  `设备ID` int(11) DEFAULT NULL,
  PRIMARY KEY (`id`),
  KEY `FK_chugl7o4iq6i0y5pffrgeredc` (`保养项目id`),
  KEY `FK_n0wn00ao1u6k70gsd99xy8xpe` (`保养人ID`),
  KEY `FK_m07tdjipwc1o5mlodow4u6gol` (`设备ID`),
  CONSTRAINT `FK_chugl7o4iq6i0y5pffrgeredc` FOREIGN KEY (`保养项目id`) REFERENCES `baoyangxiangmu` (`保养项目id`),
  CONSTRAINT `FK_m07tdjipwc1o5mlodow4u6gol` FOREIGN KEY (`设备ID`) REFERENCES `shebei` (`设备ID`),
  CONSTRAINT `FK_n0wn00ao1u6k70gsd99xy8xpe` FOREIGN KEY (`保养人ID`) REFERENCES `baoyangren` (`保养人ID`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
/*!40101 SET character_set_client = @saved_cs_client */;

--
-- Dumping data for table `baoyangjilu`
--

LOCK TABLES `baoyangjilu` WRITE;
/*!40000 ALTER TABLE `baoyangjilu` DISABLE KEYS */;
INSERT INTO `baoyangjilu` VALUES (1,NULL,NULL,1,1,1),(2,NULL,NULL,2,2,2);
/*!40000 ALTER TABLE `baoyangjilu` ENABLE KEYS */;
UNLOCK TABLES;

--
-- Table structure for table `baoyangren`
--

DROP TABLE IF EXISTS `baoyangren`;
/*!40101 SET @saved_cs_client     = @@character_set_client */;
/*!40101 SET character_set_client = utf8 */;
CREATE TABLE `baoyangren` (
  `保养人ID` int(11) NOT NULL,
  `保养人姓名` varchar(255) DEFAULT NULL,
  PRIMARY KEY (`保养人ID`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
/*!40101 SET character_set_client = @saved_cs_client */;

--
-- Dumping data for table `baoyangren`
--

LOCK TABLES `baoyangren` WRITE;
/*!40000 ALTER TABLE `baoyangren` DISABLE KEYS */;
INSERT INTO `baoyangren` VALUES (1,'张三'),(2,'李四');
/*!40000 ALTER TABLE `baoyangren` ENABLE KEYS */;
UNLOCK TABLES;

--
-- Table structure for table `baoyangxiangmu`
--

DROP TABLE IF EXISTS `baoyangxiangmu`;
/*!40101 SET @saved_cs_client     = @@character_set_client */;
/*!40101 SET character_set_client = utf8 */;
CREATE TABLE `baoyangxiangmu` (
  `保养项目id` int(11) NOT NULL,
  `保养内容` varchar(255) DEFAULT NULL,
  `设备ID` int(11) DEFAULT NULL,
  PRIMARY KEY (`保养项目id`),
  KEY `FK_j1ikfjfj9gtlha8c70fxp7f4x` (`设备ID`),
  CONSTRAINT `FK_j1ikfjfj9gtlha8c70fxp7f4x` FOREIGN KEY (`设备ID`) REFERENCES `shebei` (`设备ID`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
/*!40101 SET character_set_client = @saved_cs_client */;

--
-- Dumping data for table `baoyangxiangmu`
--

LOCK TABLES `baoyangxiangmu` WRITE;
/*!40000 ALTER TABLE `baoyangxiangmu` DISABLE KEYS */;
INSERT INTO `baoyangxiangmu` VALUES (1,'检查6000V接线盒内瓷瓶',1),(2,'接线盒内卫生清洁',2);
/*!40000 ALTER TABLE `baoyangxiangmu` ENABLE KEYS */;
UNLOCK TABLES;

--
-- Table structure for table `baoyangxiaohao`
--

DROP TABLE IF EXISTS `baoyangxiaohao`;
/*!40101 SET @saved_cs_client     = @@character_set_client */;
/*!40101 SET character_set_client = utf8 */;
CREATE TABLE `baoyangxiaohao` (
  `保养消耗Id` int(11) NOT NULL,
  `消耗数量` int(11) NOT NULL,
  `消耗材料` varchar(255) DEFAULT NULL,
  `保养记录id` int(11) DEFAULT NULL,
  PRIMARY KEY (`保养消耗Id`),
  KEY `FK_bunacx0t6sd4nkcijw2ol99xx` (`保养记录id`),
  CONSTRAINT `FK_bunacx0t6sd4nkcijw2ol99xx` FOREIGN KEY (`保养记录id`) REFERENCES `baoyangjilu` (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
/*!40101 SET character_set_client = @saved_cs_client */;

--
-- Dumping data for table `baoyangxiaohao`
--

LOCK TABLES `baoyangxiaohao` WRITE;
/*!40000 ALTER TABLE `baoyangxiaohao` DISABLE KEYS */;
/*!40000 ALTER TABLE `baoyangxiaohao` ENABLE KEYS */;
UNLOCK TABLES;

--
-- Table structure for table `shebei`
--

DROP TABLE IF EXISTS `shebei`;
/*!40101 SET @saved_cs_client     = @@character_set_client */;
/*!40101 SET character_set_client = utf8 */;
CREATE TABLE `shebei` (
  `设备ID` int(11) NOT NULL,
  `保养周期` varchar(255) DEFAULT NULL,
  `备注` varchar(255) DEFAULT NULL,
  `最后保养时间` datetime DEFAULT NULL,
  `设备名称` varchar(255) DEFAULT NULL,
  `设备类型id` int(11) DEFAULT NULL,
  PRIMARY KEY (`设备ID`),
  KEY `FK_pyttby5p42aplcrcg3unk1aeq` (`设备类型id`),
  CONSTRAINT `FK_pyttby5p42aplcrcg3unk1aeq` FOREIGN KEY (`设备类型id`) REFERENCES `shebeileixing` (`设备类型Id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
/*!40101 SET character_set_client = @saved_cs_client */;

--
-- Dumping data for table `shebei`
--

LOCK TABLES `shebei` WRITE;
/*!40000 ALTER TABLE `shebei` DISABLE KEYS */;
INSERT INTO `shebei` VALUES (1,'1',NULL,NULL,'防冻液喷洒设备',1),(2,'2',NULL,NULL,'防冻设备',1),(3,'3',NULL,NULL,'变压器',1),(4,'4',NULL,NULL,'浓缩机',1);
/*!40000 ALTER TABLE `shebei` ENABLE KEYS */;
UNLOCK TABLES;

--
-- Table structure for table `shebeileixing`
--

DROP TABLE IF EXISTS `shebeileixing`;
/*!40101 SET @saved_cs_client     = @@character_set_client */;
/*!40101 SET character_set_client = utf8 */;
CREATE TABLE `shebeileixing` (
  `设备类型Id` int(11) NOT NULL,
  `设备类型` varchar(255) DEFAULT NULL,
  PRIMARY KEY (`设备类型Id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
/*!40101 SET character_set_client = @saved_cs_client */;

--
-- Dumping data for table `shebeileixing`
--

LOCK TABLES `shebeileixing` WRITE;
/*!40000 ALTER TABLE `shebeileixing` DISABLE KEYS */;
INSERT INTO `shebeileixing` VALUES (1,'6000V以下不带振动电机');
/*!40000 ALTER TABLE `shebeileixing` ENABLE KEYS */;
UNLOCK TABLES;

--
-- Table structure for table `zhouqi`
--

DROP TABLE IF EXISTS `zhouqi`;
/*!40101 SET @saved_cs_client     = @@character_set_client */;
/*!40101 SET character_set_client = utf8 */;
CREATE TABLE `zhouqi` (
  `周期ID` int(11) NOT NULL,
  `保养期` int(11) NOT NULL,
  `提前期` int(11) NOT NULL,
  PRIMARY KEY (`周期ID`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
/*!40101 SET character_set_client = @saved_cs_client */;

--
-- Dumping data for table `zhouqi`
--

LOCK TABLES `zhouqi` WRITE;
/*!40000 ALTER TABLE `zhouqi` DISABLE KEYS */;
INSERT INTO `zhouqi` VALUES (1,7,1),(2,30,2),(3,180,7),(4,365,14);
/*!40000 ALTER TABLE `zhouqi` ENABLE KEYS */;
UNLOCK TABLES;
/*!40103 SET TIME_ZONE=@OLD_TIME_ZONE */;

/*!40101 SET SQL_MODE=@OLD_SQL_MODE */;
/*!40014 SET FOREIGN_KEY_CHECKS=@OLD_FOREIGN_KEY_CHECKS */;
/*!40014 SET UNIQUE_CHECKS=@OLD_UNIQUE_CHECKS */;
/*!40101 SET CHARACTER_SET_CLIENT=@OLD_CHARACTER_SET_CLIENT */;
/*!40101 SET CHARACTER_SET_RESULTS=@OLD_CHARACTER_SET_RESULTS */;
/*!40101 SET COLLATION_CONNECTION=@OLD_COLLATION_CONNECTION */;
/*!40111 SET SQL_NOTES=@OLD_SQL_NOTES */;

二、er图链接
http://pan.baidu.com/s/1skQdNJJ
三、Axure原型链接
http://pan.baidu.com/s/1hsbl43M
