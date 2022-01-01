<template>
    
    <div class="phone-wrap">
        <div class="phone clearfix">
            <div class="screen">

                <div class="top">
                    12.35
                    &nbsp;
                    <i class="ion-social-instagram-outline"></i>
                    {{}}
                    <i class="ion-more"></i>

                    <i class="ion-ios-alarm-outline" style="right:75px; margin-top:1px; position:absolute;"></i>
                    <i class="ion-wifi" style="right:55px; margin-top:0px; position:absolute;"></i>
                    <i class="ion-connection-bars" style="right:40px; position:absolute;"></i>
                    <i class="ion-battery-full" style="right:20px; margin-top:1.8px; position:absolute;"></i>
                </div>
                
                <div class="text-blue-300 font-bold text-center text-3xl mb-7 mt-3 mr-4">
                    NCS Music Player
                </div>
            
                <div class="play">
                    <section class="player">
                        <h2 class="song-title">
                            {{ current.title }} - 
                            <span>
                                {{ current.artist }}
                            </span>
                        </h2>

                        <div class="part">
                            <div class="grid grid-cols-3 mt-10">

                                <div class="flex items-center justify-center">
                                    <button 
                                        @click="prev"
                                    >
                                        <i class="ion-ios-skipbackward"></i>
                                    </button>
                                </div>

                                <div class="flex items-center justify-center">
                                    <button 
                                        class="rounded-full bg-white h-10 w-10 text-black font-bold" 
                                        v-if="!isPlaying" 
                                        @click="play"
                                    >
                                        <div class="play-btn">
                                            <i class="ion-ios-play"></i>
                                        </div>
                                        
                                    </button>

                                    <button 
                                        class="rounded-full bg-white h-10 w-10 text-black font-bold" 
                                        v-else 
                                        @click="pause"
                                    >
                                        <i class="ion-ios-pause"></i>
                                    </button>
                                </div>

                                <div class="flex items-center justify-center">
                                    <button class="next" @click="next">
                                        <i class="ion-ios-skipforward"></i>
                                    </button>
                                </div>

                            </div>
                        </div>
                        

                    </section>
                </div>

                <div class="line">

                </div>

                <div class="choose">
                    <section class="playlist">
                        <h3>Available Songs</h3>
                        <button v-for="song in songs" :key="song.src" @click="play(song)" :class="(song.src == current.src) ? 'song playing' : 'song'">
                            <div class="flex flex-row mb-4">

                                <div class="logo">
                                    <img
                                        class="max-h-12 rounded"
                                        src="../assets/ncs.png"
                                    />
                                </div>

                                <div class="info">
                                    <div class="title-name">
                                        {{ song.title }}
                                    </div>
                                    
                                    <br>

                                    <div class="creator-name">
                                        {{ song.artist }} 
                                    </div>         
                                </div>

                                <div class="like">
                                    <i v-if="this.index===0" class="ion-android-favorite"></i>
                                    <i v-else class="ion-android-favorite-outline"></i>
                                </div>
                                
                            </div>
                        </button>

                    </section>
                </div>

                <div class="footer">
                    <i class="ion-android-arrow-back"></i>
                    {{}}
                    <i class="ion-android-home"></i>
                    {{}}
                    <i class="ion-android-apps"></i>
                </div>
                
            </div>

        </div>
    </div>

</template>

<script>
    export default {
        data () {
            return {
                current: {},
                index: 0,
                isPlaying: false,
                songs: [
                    {
                    title: 'Heroes Tonight',
                    artist: 'Janji',
                    src: require('../assets/one.mp3')
                    },
                    {
                    title: 'Adventure',
                    artist: 'JJD',
                    src: require('../assets/two.mp3')
                    },
                    {
                    title: 'Heart A Fire',
                    artist: 'Defqwop',
                    src: require('../assets/three.mp3')
                    }
                ],
                player: new Audio()
            }
        },
        methods: {
            play(song) {
                this.$emit("goto", 1);
                if (typeof song.src != "undefined") {
                    this.current = song;
                    this.player.src = this.current.src;
                }

                this.player.play();
                this.player.volume = 0.2;

                this.player.addEventListener('ended', function () {
                    this.index++;
                    if (this.index > this.songs.length - 1) {
                    this.index = 0;
                    }
                    this.current = this.songs[this.index];
                    this.play(this.current);
                }.bind(this));
                this.isPlaying = true;
            },

            pause() {
                this.player.pause();
                this.isPlaying = false;
            },

            next() {
                this.index++;
                if (this.index > this.songs.length - 1) {
                    this.index = 0;
                }
                this.current = this.songs[this.index];
                this.play(this.current);
            },
            
            prev() {
                this.index--;
                if (this.index < 0) {
                    this.index = this.songs.length - 1;
                }
                this.current = this.songs[this.index];
                this.play(this.current);
            }
        },
        created() {
            this.current = this.songs[this.index];
            this.player.src = this.current.src;
        }
    }
</script>

<style>
    
</style>